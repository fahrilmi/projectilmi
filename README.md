# RITME (by Project Ilmi)

> **The Operating System for Recurring Community Fitness**  
> Engineered for Poundfit, Yoga, Pilates, Functional Training & Running Clubs.  
> 🌐 **Live Website:** [projectilmi.web.id](https://projectilmi.web.id) (Mirror: [fahrilmi.github.io/projectilmi](https://fahrilmi.github.io/projectilmi/))

---

## ⚡ Executive Summary (Investor Pitch)

Pasca-pandemi, terjadi pergeseran masif dari gym komersial konvensional ke arah **Boutique & Community Fitness** yang berbasis kelas berulang mingguan. Di Indonesia saja, terdapat lebih dari **45.000 komunitas olahraga aktif** yang masih dikelola secara manual lewat chat WhatsApp, transfer rekening tercecer, dan foto dokumentasi 600+ yang terkubur di Google Drive.

**RITME** mengotomasi seluruh siklus kelas komunitas dengan model **Zero Upfront Cost** dan **2.5% take rate** per transaksi.

---

## 🚀 Key Advantages (Cara Lama vs RITME)

| Dimensi Operasional | Cara Konvensional (WA & GDrive) | Platform Tiket Konser | RITME by Project Ilmi |
|---|---|---|---|
| **Biaya Host** | Gratis (habis 15+ jam/minggu admin) | Potongan komisi 5% - 10% | **Rp 0 di muka + 2.5% fee per tiket** |
| **Pendaftaran & Bayar** | Chat satu-satu & kirim bukti transfer | Web checkout generik | **1-Klik Booking + Dynamic QRIS** |
| **Distribusi Foto** | Google Drive 600+ foto lambat | Tidak ada fitur foto | **SnapFind AI: Wajah terdeteksi < 300ms** |
| **Notifikasi WhatsApp** | Broadcast manual rawan banned | Hanya lewat email | **WhatsApp Cloud API: Tiket QR & Notif Foto** |
| **Absensi Pintu** | Kertas basah / checklist manual | Sewa scanner barcode mahal | **Fast Camera Scan di HP panitia** |
| **Retensi Member** | Tidak ada (member hilang) | Tidak ada (transaksi putus) | **Streak Flame 🔥 & Milestone Badges** |
| **Bagi Hasil Coach** | Hitung manual di akhir bulan | Tidak didukung | **Auto Splitter kalkulasi fee coach & laba** |

---

## 🏗️ Core Architecture & Deep-Tech Pillars

1. **SnapFind AI Facial Recognition Engine:**
   - Model: MobileFaceNet 512-dimensi normalized embeddings.
   - Vector Search: PostgreSQL dengan ekstensi `pgvector` & HNSW indexing (< 250ms cosine similarity).
   - Storage: Cloudflare R2 dengan **$0 Egress Bandwidth Cost**.
   - Social Ready: Export preset format 9:16 untuk Instagram Stories.

2. **WhatsApp Cloud API Notification Gateway:**
   - Pengiriman dynamic QR Ticket instan ke chat WhatsApp peserta.
   - Pengingat otomatis H-2 jam sebelum kelas.
   - Notifikasi broadcast pasca-event saat foto selesai diproses AI.

3. **High-Craft Design Engineering:**
   - Dibangun dengan standar desain **Emil Kowalski (mantan desainer Vercel/Linear)**.
   - Micro-interactions haptik (`scale(0.97)` on `:active`), custom cubic-bezier easing, zero AI-slop, dan estetika obsidian athletic dark mode.

---

## 📊 Market Opportunity (Indonesia)

- **Total Addressable Market (TAM):** $2.4 Miliar wellness & sports economy (8.9% CAGR).
- **Serviceable Available Market (SAM):** 45.000+ komunitas olahraga berulang independen (~Rp 5.2 Triliun GMV potensial).
- **Serviceable Obtainable Market (SOM - 18 Bulan):** 1.500 komunitas aktif di Jawa Timur & Jabodetabek (Target GMV Rp 175.5 Miliar / ARR Platform Rp 4.38 Miliar).

---

## 📂 Repository Structure

```
.
├── CNAME                         # Custom domain mapping (projectilmi.web.id)
├── index.html                    # Investor Pitch & Live Prototype (Root for Pages)
├── public/
│   └── index.html                # Standalone preview bundle
├── docs/
│   ├── PRD.md                    # Product Requirement Document (Investor Edition)
│   ├── STYLE_GUIDE.md            # Emil Kowalski & Impeccable Design System Specs
│   └── TECHNICAL_REQUIREMENTS.md # Arsitektur Teknis, DDL Database & API Endpoints
└── README.md
```

---

## 👨‍💻 Founder & Project Lead

**Fahril Haikal Ilmi Sihabudin**  
- Founder of Project Ilmi ([projectilmi.web.id](https://projectilmi.web.id))
- Pelaksana Seksi Pengawasan KPP Pratama Kediri (DJP)
- AI & Autonomous Agent System Architect
- Grassroots Community Collaborator (@poundiri.team)
- GitHub: [@fahrilmi](https://github.com/fahrilmi)
