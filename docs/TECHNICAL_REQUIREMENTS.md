# Technical Requirement Document (TRD)

## Project Name: RITME (by Project Ilmi)
**Document Version:** 1.0.0  
**Target Environment:** Cloudflare Edge + Hybrid Micro-backend  
**Author:** Fahril Haikal Ilmi Sihabudin (projectilmi.web.id)  
**Status:** Approved for Architecture & Prototyping  

---

## 1. System Architecture Overview

RITME utilizes a modern, cost-efficient **Jamstack & Micro-service Hybrid Architecture** designed to handle spiky traffic (mass registrations when slots open) and data-intensive AI operations (bulk face vector search) with near-zero idle infrastructure cost:

```
[ Mobile / Desktop Browser (Participant & Host PWA) ]
                      │
                      ▼ HTTPS / WebSocket
         [ Cloudflare Global CDN / Edge ]
      ┌───────────────┴───────────────┐
      ▼                               ▼
[ Cloudflare Pages ]           [ Cloudflare Workers / API Gateway ]
(Static Frontend Assets)       (Auth Validation & Fast Caching)
                                      │
                      ┌───────────────┴───────────────┐
                      ▼                               ▼
          [ FastAPI Core Backend ]          [ Cloudflare R2 Storage ]
       (Business Logic, Booking Engine,     (Zero Egress Photo Buckets
        WhatsApp Webhooks & Midtrans)        & High-Res Originals)
                      │                               │
                      ▼                               ▼
        [ PostgreSQL with pgvector ]      [ SnapFind AI Biometric Engine ]
     (Relational Data, Event Schemas,     (Face Detection, MobileFaceNet
       User Profiles & 512-D Vectors)     Embedding & Cosine Similarity)
```

---

## 2. Technology Stack & Component Selection

### 2.1 Frontend Client (Mobile PWA & Host Dashboard)
- **Framework:** Next.js (App Router) or Vite + React / Astro for static marketing pages.
- **Styling:** Tailwind CSS v4 configured with the RITME Athletic Design System tokens (`#08090A`, `#D4FF00`, `#00F0FF`).
- **State & Data Fetching:** TanStack Query (React Query) for optimistic UI updates and cache invalidation during slot booking.
- **Icons & Assets:** Lucide React (clean, geometric line icons, zero visual clutter).
- **PWA Capabilities:** Service Worker caching for offline ticket display, installable app banner, camera stream integration for QR check-in scanner.

### 2.2 Backend & API Services
- **Core API Framework:** **FastAPI (Python 3.11+)**
  - *Rationale:* Native asynchronous performance (`asyncio`), automated OpenAPI documentation, seamless integration with Python-based AI biometrics libraries without cross-language overhead.
- **Validation & Schemas:** Pydantic v2 for high-speed serialization and request payload validation.
- **Background Tasks:** Celery / ARQ (Async Redis Queue) for non-blocking photo ingestion, face crop processing, and batch WhatsApp reminders.

### 2.3 Database & Storage Layer
- **Primary Database:** **PostgreSQL 16+** with **`pgvector`** extension.
  - Relational schema handles users, recurring schedules, bookings, transactions, and check-in logs.
  - `vector(512)` column stores facial embeddings indexed with HNSW (Hierarchical Navigable Small World) for sub-second nearest-neighbor similarity search.
- **Object Storage (Photos & Assets):** **Cloudflare R2**
  - *Key Advantage:* **Zero egress fees**. When 100 participants download 20MB of high-res photos each, bandwidth costs remain $0.
- **Image CDN & Optimization:** Cloudflare Images / WebP compression pipeline to generate instant 300px thumbnails for the search results feed.

### 2.4 AI Biometrics Pipeline (SnapFind AI Engine)
- **Face Detector:** SCRFD (Sample and Computation Redistribution for Efficient Face Detection) or RetinaFace running on ONNX Runtime (CPU-optimized, low RAM footprint).
- **Face Embedding Model:** MobileFaceNet / ArcFace (512-dimensional normalized float vectors).
- **Search Pipeline:**
  1. Participant uploads 1 selfie via mobile browser.
  2. Client-side or edge lightweight detection extracts the user's face crop.
  3. Embedding extracted: `vector = extract_embedding(face_img)`.
  4. SQL Query via pgvector:
     ```sql
     SELECT photo_id, url, thumbnail_url, (embedding <=> $1) AS distance
     FROM event_face_embeddings
     WHERE event_id = $2 AND (embedding <=> $1) < 0.42
     ORDER BY distance ASC
     LIMIT 50;
     ```
  5. Response returns matched photo URLs to the client in `< 250ms`.

### 2.5 Payments & Financial Operations
- **Payment Gateway:** Midtrans Snap API / Xendit Invoicing API.
  - Payment Methods: QRIS Dinamis (GoPay, ShopeePay, BCA, Dana), Virtual Accounts (BCA, Mandiri, BRI, BNI).
  - Webhook Listener: Signed webhook validation to verify transaction status (`settlement`, `expire`, `cancel`) and automatically release or confirm slot reservations.

### 2.6 Messaging & Automated Notification Engine
- **WhatsApp Gateway:** WhatsApp Business Cloud API or self-hosted Baileys / Fonnte service.
  - **Trigger 1 (Instant Booking):** Kirim tiket digital + dynamic QR code + link kalender (.ics) segera setelah pembayaran sukses.
  - **Trigger 2 (H-2 Jam Reminder):** Notifikasi jadwal + tips persiapan (bawa matras/ripstix).
  - **Trigger 3 (Post-Class Magic):** "Foto kelas tadi sudah ready! Tap link ini untuk scan wajahmu dan download fotomu 📸".

---

## 3. Database Schema Blueprint (PostgreSQL)

```sql
-- 1. Users Table
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    full_name VARCHAR(100) NOT NULL,
    phone_number VARCHAR(20) UNIQUE NOT NULL,
    email VARCHAR(120),
    avatar_url TEXT,
    streak_count INT DEFAULT 0,
    total_classes_attended INT DEFAULT 0,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- 2. Communities / Hosts Table
CREATE TABLE communities (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(100) NOT NULL,
    slug VARCHAR(60) UNIQUE NOT NULL,
    description TEXT,
    logo_url TEXT,
    whatsapp_contact VARCHAR(20),
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- 3. Recurring Class Programs
CREATE TABLE class_programs (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    community_id UUID REFERENCES communities(id) ON DELETE CASCADE,
    title VARCHAR(120) NOT NULL, -- e.g. "Poundfit Sunset Kediri"
    category VARCHAR(50) NOT NULL, -- "Poundfit", "Yoga", "Pilates"
    instructor_name VARCHAR(100) NOT NULL,
    default_price NUMERIC(10, 2) NOT NULL,
    default_capacity INT NOT NULL DEFAULT 30,
    venue_name VARCHAR(150) NOT NULL,
    venue_address TEXT
);

-- 4. Specific Class Sessions (Instances of recurring programs)
CREATE TABLE class_sessions (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    program_id UUID REFERENCES class_programs(id) ON DELETE CASCADE,
    start_time TIMESTAMP WITH TIME ZONE NOT NULL,
    end_time TIMESTAMP WITH TIME ZONE NOT NULL,
    capacity INT NOT NULL,
    booked_count INT NOT NULL DEFAULT 0,
    status VARCHAR(20) DEFAULT 'OPEN', -- 'OPEN', 'FULL', 'CANCELLED', 'COMPLETED'
    is_photo_ready BOOLEAN DEFAULT FALSE
);

-- 5. Bookings & Tickets
CREATE TABLE bookings (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    session_id UUID REFERENCES class_sessions(id) ON DELETE RESTRICT,
    user_id UUID REFERENCES users(id) ON DELETE RESTRICT,
    booking_code VARCHAR(12) UNIQUE NOT NULL,
    amount_paid NUMERIC(10, 2) NOT NULL,
    payment_status VARCHAR(20) NOT NULL, -- 'PENDING', 'PAID', 'EXPIRED', 'REFUNDED'
    payment_method VARCHAR(30),
    qr_token TEXT NOT NULL,
    checked_in BOOLEAN DEFAULT FALSE,
    checked_in_at TIMESTAMP WITH TIME ZONE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- 6. Event Photos & Face Embeddings (SnapFind Integration)
CREATE TABLE event_photos (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    session_id UUID REFERENCES class_sessions(id) ON DELETE CASCADE,
    storage_key TEXT NOT NULL,
    public_url TEXT NOT NULL,
    thumbnail_url TEXT NOT NULL,
    uploaded_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

CREATE TABLE event_face_embeddings (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    photo_id UUID REFERENCES event_photos(id) ON DELETE CASCADE,
    session_id UUID REFERENCES class_sessions(id) ON DELETE CASCADE,
    bounding_box JSONB NOT NULL, -- [x1, y1, x2, y2]
    embedding vector(512) NOT NULL -- pgvector
);

-- Vector Index for Sub-second Similarity Search
CREATE INDEX idx_face_embeddings_hnsw 
ON event_face_embeddings 
USING hnsw (embedding vector_cosine_ops)
WITH (m = 16, ef_construction = 64);
```

---

## 4. API Specification (Core Endpoints)

### Booking & Sessions API
- `GET /api/v1/communities/:slug/sessions` — Mendapatkan jadwal kelas aktif (mendukung filter tanggal & kategori).
- `POST /api/v1/sessions/:id/book` — Inisialisasi booking & pembuatan invoice pembayaran Midtrans QRIS.
- `POST /api/v1/webhooks/payments` — Menerima notifikasi settlement dari payment gateway.
- `GET /api/v1/tickets/:code` — Render detail tiket & QR code check-in.

### Check-in Ops API
- `POST /api/v1/ops/scan-checkin` — Validasi scan QR code peserta oleh panitia di lokasi (latensi < 100ms).
- `GET /api/v1/ops/sessions/:id/roster` — Live real-time attendee list dengan status check-in.

### SnapFind AI Biometrics API
- `POST /api/v1/sessions/:id/photos/bulk-upload` — Upload batch foto oleh fotografer (menghasilkan background vectorization task).
- `POST /api/v1/sessions/:id/photos/face-search` — Menerima foto selfie peserta, mengekstrak embedding, dan mengembalikan array foto yang cocok dengan cosine similarity > 0.65.

---

## 5. Security, Privacy & Reliability

1. **Biometric Privacy Safeguards:**
   - Foto selfie peserta yang digunakan untuk pencarian galeri **tidak disimpan permanen** atau digunakan untuk melatih model umum.
   - Vektor embedding 512-D adalah data satu arah (one-way representation) yang tidak dapat direkonstruksi kembali menjadi foto wajah asli.
2. **Rate Limiting & Fraud Prevention:**
   - Pembatasan request booking per IP untuk mencegah bot ticket hoarding saat pendaftaran kelas dibuka.
   - Idempotency key pada setiap inisialisasi pembayaran untuk mencegah double charge.
3. **High Availability During Rush Hours:**
   - Caching jadwal sesi dan kuota di Cloudflare Edge Cache / Redis untuk menahan lonjakan ribuan klik saat jadwal kelas mingguan baru diumumkan di Instagram.

---

## 6. Budget & Infrastructure Sizing (MVP to 10k Monthly Members)

| Komponen | Provider / Tier | Estimasi Biaya / Bulan |
|---|---|---|
| **Frontend & DNS** | Cloudflare Pages + DNS (Domain `projectilmi.web.id`) | **Rp 0** (Free Tier) |
| **Object Storage (Foto)** | Cloudflare R2 (10 GB free + 0 egress) | **Rp 0** (Free Tier) |
| **Database & Vectors** | Neon / Supabase PostgreSQL with pgvector | **Rp 0** (Free Tier hingga 500MB) |
| **Backend & AI Worker** | AWS EC2 t3.small (existing instance) / Fly.io | **Rp 0** (Memanfaatkan server saat ini) |
| **WhatsApp Notification** | Fonnte / WhatsApp Gateway API | Rp 50.000 - Rp 100.000 |
| **Payment Gateway** | Midtrans (Fee per transaksi 0.7% QRIS) | Pay-as-you-go |
| **Total Estimasi MVP** | | **< Rp 100.000 / bulan** |
