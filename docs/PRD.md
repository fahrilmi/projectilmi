# Product Requirement Document (PRD) — Investor & Execution Edition

## Project Name: RITME (by Project Ilmi)
**Tagline:** The Operating System for Recurring Sports Classes & Community Fitness  
**Domain:** `projectilmi.web.id`  
**Founder:** Fahril Haikal Ilmi Sihabudin  
**Stage:** Pre-Seed / Architecture & Seed Prototype  
**Target Market:** Indonesia & Southeast Asia Recurring Boutique Fitness  
**Document Version:** 2.0.0-investor-ready  

---

## 1. Executive Summary & Pitch Narrative

### 1.1 The "Why Now" (Market Phenomenon)
Pasca-pandemi, terjadi pergeseran masif dari gym komersial konvensional berbayar bulanan mahal ke arah **Boutique & Community Fitness** yang berbasis kelas berulang: **Poundfit, Mat Pilates, Vinyasa Yoga, Functional/Hyrox, Padel, dan Running Clubs**.

Di Indonesia saja, ribuan kelas komunitas diadakan setiap minggu di sewa studio, lapangan terbuka, rooftop mall, hingga aula serbaguna. Namun, **90% pengelola komunitas ini masih beroperasi secara primitif**:
1. **Manual WhatsApp Booking Chaos:** Pendaftaran lewat DM WhatsApp satu per satu, transfer manual rekening BCA, dan pencatatan di Google Sheets.
2. **Dokumentasi Terkubur di Google Drive (600+ Foto):** Fotografer mengunggah foto ke folder Google Drive. Member malas download karena harus menyaring ratusan foto untuk mencari dirinya sendiri, sehingga momentum promosi organik di Instagram Stories hilang.
3. **High Churn / Member Drop-out:** Komunitas tidak memiliki sistem retensi (gamifikasi, konsistensi habit, reward milestone).
4. **Alat Eksisting Tidak Cocok:** Software gym luar negeri (Mindbody, Glofox) membebankan biaya tetap bulanan yang sangat mahal ($150 - $300/bulan) dan terlalu kaku untuk kelas komunitas sewa venue independen. Sebaliknya, platform tiket konser (Loket, Megatix) mengambil komisi besar (5-10%) dan tidak memiliki fitur absensi berulang, absensi WhatsApp, maupun pengiriman foto AI.

### 1.2 The Solution: RITME
**RITME** adalah all-in-one OS mobile-first yang mengotomasi seluruh siklus kelas olahraga mingguan:
- **Zero-Friction Scheduling & Payments:** Booking mandiri dalam 15 detik via QRIS dengan konfirmasi otomatis.
- **SnapFind AI Instant Face Delivery:** Member upload selfie 1x, semua foto aksinya dari 500+ galeri fotografer langsung ditemukan dalam hitungan milidetik dan siap dibagikan ke Instagram Stories dengan preset 9:16.
- **WhatsApp Cloud API Integration:** Dynamic QR Ticket, pengingat H-2 jam, dan notifikasi foto otomatis langsung masuk ke chat personal peserta.
- **Habit Gamification:** Streak mingguan, milestone badges, dan sponsor benefits digital.

---

## 2. Market Opportunity & Size (TAM / SAM / SOM)

### 2.1 Total Addressable Market (TAM)
- **Industri Olahraga & Kebugaran Indonesia:** Bernilai lebih dari **$2.4 Miliar (Rp 38 Triliun)** dengan pertumbuhan tahunan (CAGR) 8.9% hingga 2030 (sumber: Statista & Wellness Institute SEA).

### 2.2 Serviceable Available Market (SAM)
- **Komunitas & Studio Kebugaran Boutique Independen di Kota Tier 1 & Tier 2:**
  - Terdapat lebih dari **45.000 komunitas olahraga aktif** di Indonesia (Jabodetabek, Surabaya, Malang, Kediri, Bandung, Semarang, Medan, Bali) yang mengadakan kelas rutin minimal 2x seminggu.
  - Estimasi volume tiket mingguan: 45.000 komunitas × rata-rata 25 peserta × 2 sesi/minggu = **2.250.000 transaksi tiket per minggu**.
  - Nilai Transaksi Bruto (GMV) Potensial: Rp 45.000/tiket × 2.25M transaksi/minggu × 52 minggu = **Rp 5.2 Triliun GMV / tahun**.

### 2.3 Serviceable Obtainable Market (SOM) — Target 18 Bulan Pertama
- Fokus geografis: **Jawa Timur (Kediri, Surabaya, Malang) & Jabodetabek**.
- Target: **1.500 Komunitas Aktif (Poundfit, Yoga, Running Club)**.
- Target Transaksi: 1.500 komunitas × 25 peserta × 2 sesi/minggu = 75.000 tiket/minggu (~3.9 Juta tiket/tahun).
- Nilai GMV Tahunan: 3.9 Juta × Rp 45.000 = **Rp 175.5 Miliar GMV**.
- Proyeksi Revenue Platform (pada 2.5% take rate): **Rp 4.38 Miliar / tahun (ARR)**.

---

## 3. Business Model & Pricing Strategy

RITME menerapkan filosofi **"No Barrier to Adopt"** — pengelola komunitas tidak perlu membayar biaya langganan bulanan di muka (*Zero Upfront Cost*).

| Paket Layanan | Biaya Langganan Bulanan | Biaya Transaksi (Platform Fee) | Fitur Utama |
|---|---|---|---|
| **Community Starter** | **Rp 0 / GRATIS SELAMANYA** | **2.5% per transaksi tiket berhasil** | • Jadwal kelas berulang tak terbatas<br>• Integrasi pembayaran QRIS & e-Wallet otomatis<br>• Dynamic QR Ticket delivery via WhatsApp<br>• SnapFind AI Photo Search (hingga 1.000 foto/bulan)<br>• QR Scanner absensi panitia<br>• Rekap keuangan otomatis |
| **Studio Pro & Multi-Venue** | **Rp 299.000 / bulan** | **1.8% per transaksi tiket** | • Semua fitur Starter<br>• Custom sender WhatsApp (Official Brand Name)<br>• Multi-instruktur & split payout otomatis ke bank coach<br>• SnapFind AI Unlimited Foto<br>• Custom branding watermark di IG Story export<br>• Dedicated account manager |
| **Sponsorship Network (Add-on)** | Revenue Share (15% dari nilai voucher/deal) | — | • Marketplace penempatan voucher produk sponsor (minuman isotonik, apparel, healthy catering) di dashboard peserta. |

### Mengapa Model 2.5% Sangat Menarik Bagi Host?
- **Host tidak mengambil risiko rugi:** Jika kelas libur atau sedang sedikit peserta, host tidak dibebani biaya operasional software.
- Biaya 2.5% dari tiket Rp 45.000 hanyalah **Rp 1.125** — jauh lebih murah dibanding tenaga dan waktu admin yang terbuang berjam-jam membalas chat WA pendaftaran.

---

## 4. Competitive Matrix: Cara Lama vs RITME

| Dimensi Operasional | Cara Lama (Manual WhatsApp & GDrive) | Platform Tiket Konser (Loket, Megatix) | Software Gym Asing (Mindbody, Glofox) | **RITME by Project Ilmi** |
|---|---|---|---|---|
| **Biaya untuk Host** | Gratis (tapi makan waktu admin 15 jam/minggu) | Potongan besar **5% - 10%** per tiket | Biaya tetap mahal **$150 - $300/bln** (Rp 2.5jt - 5jt/bln) | **GRATIS di awal + hanya 2.5% per transaksi** |
| **Pendaftaran & Pembayaran** | Manual chat WhatsApp, kirim bukti transfer, cek mutasi bank manual | Web form umum, tidak ada konteks komunitas | App store download wajib, setup kompleks | **1-Klik Booking via Web PWA + Dynamic QRIS instan** |
| **Pembagian Foto Dokumentasi** | Link Google Drive 600+ foto, kuota penuh, peserta pusing scroll | Tidak ada fitur foto | Tidak ada fitur foto | **SnapFind AI: Selfie 1 detik, semua foto aksi langsung terdeteksi (< 300ms)** |
| **Integrasi WhatsApp** | Manual copy-paste broadcast, sering diblokir WhatsApp | Email konfirmasi tiket (sering masuk spam) | Email / Push notif in-app | **Native WhatsApp Cloud API: E-Pass QR, H-2 Jam Reminder & Notif Foto AI** |
| **Absensi di Lokasi** | Kertas checklist manual (mudah basah/hilang) | Barcode scanner mahal | RFID card / Fingerprint statis di pintu | **Fast Camera QR Scanner di smartphone panitia + WhatsApp Self Check-in** |
| **Retensi & Kebiasaan** | Nol — member datang 1-2 kali lalu hilang | Nol — model transaksi sekali putus | Standar point system | **Weekly Streak Flame 🔥, Milestone Badges & Voucher Sponsor Otomatis** |
| **Bagi Hasil Instruktur** | Rekap spreadsheet manual di akhir bulan | Tidak didukung | Modul payroll rumit | **Smart Splitter: Real-time calculation fee coach & laba bersih per sesi** |

---

## 5. Core Architectural Pillars

### 5.1 Pillar A: SnapFind Biometric AI Engine
- **Algoritma:** MobileFaceNet / ArcFace (512-D Normalized Vector Embeddings).
- **Indexing:** `pgvector` dengan HNSW cosine similarity search.
- **Workflow:**
  1. Fotografer drag-and-drop 500 foto ke Cloudflare R2 via portal host.
  2. Background worker mengekstrak koordinat wajah dan membuat 512-D embedding.
  3. Peserta mengambil selfie 1 kali di browser mobile.
  4. Query vektor mencocokkan kemiripan wajah dalam tempo `< 250ms`.
  5. Peserta mendapatkan personal gallery dan 1-tap download dengan preset 9:16 siap posting ke Instagram Stories.

### 5.2 Pillar B: WhatsApp Real-Time Notification Pipeline
- **Ticketing Delivery:** Segera setelah pembayaran QRIS settlement, webhook memicu bot WhatsApp mengirimkan gambar QR Ticket, kode booking, dan link kalender.
- **Pre-Event Engagement:** Pesan pengingat personal H-2 jam (lokasi Maps, barang yang wajib dibawa).
- **Post-Event Magic Moment:** Maksimal 30 menit setelah fotografer mengunggah foto, seluruh peserta terdaftar menerima pesan: *"Hai Nadya! Foto aksimu di kelas tadi malam sudah ready! Klik link ini untuk scan wajahmu 📸"*.

### 5.3 Pillar C: Habit Engine & Digital Sponsor Perks
- **Streak Logic:** Sistem menghitung kehadiran mingguan tanpa putus.
- **Tiered Badges:** *First Beat* (1x), *5x Rebel* (klaim tumbler/merchandise), *20x Warrior* (diskon pass 25%).
- **Targeted Perks:** Brand partner dapat menargetkan voucher secara spesifik ke peserta yang terverifikasi hadir di lokasi, menghasilkan conversion rate 5x lipat lebih tinggi dibanding brosur atau banner fisik.

---

## 6. Financial Projections & Unit Economics (3-Year Horizon)

| Metrik | Tahun 1 (Pilot Jatim) | Tahun 2 (Ekspansi Jawa) | Tahun 3 (Nasional & SEA) |
|---|---|---|---|
| **Komunitas Aktif** | 500 | 2.500 | 10.000 |
| **Tiket Terjual / Tahun** | 1.300.000 | 6.500.000 | 26.000.000 |
| **Gross Merchandise Value (GMV)** | Rp 58,5 Miliar | Rp 292,5 Miliar | Rp 1,17 Triliun |
| **Net Revenue (2.5% Take Rate)** | **Rp 1,46 Miliar** | **Rp 7,31 Miliar** | **Rp 29,25 Miliar** |
| **Gross Margin** | 82% | 86% | 89% |
| **Infrastruktur Bulanan (R2 + Cloudflare + Server)** | ~Rp 1,5 Juta | ~Rp 8 Juta | ~Rp 35 Juta |
