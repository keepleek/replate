# 🍽️ REPLATE — Give Surplus Food Another Route

<p align="center">
  <img src="https://img.shields.io/badge/Status-Live%20on%20Vercel-success?style=for-the-badge&logo=vercel" alt="Vercel Status" />
  <img src="https://img.shields.io/badge/Backend%20API-Live%20on%20VPS-blue?style=for-the-badge&logo=nestjs" alt="VPS Status" />
  <img src="https://img.shields.io/badge/Food%20Safety%20Gate-WHO%20%E2%80%A2%20Kemenkes%20%E2%80%A2%20BPOM-teal?style=for-the-badge" alt="Food Safety Gate" />
  <img src="https://img.shields.io/badge/React-19.2-61dafb?style=for-the-badge&logo=react" alt="React 19" />
  <img src="https://img.shields.io/badge/NestJS-10.4-e0234e?style=for-the-badge&logo=nestjs" alt="NestJS" />
  <img src="https://img.shields.io/badge/Prisma-5.22-2d3748?style=for-the-badge&logo=prisma" alt="Prisma ORM" />
  <img src="https://img.shields.io/badge/PostgreSQL-16-336791?style=for-the-badge&logo=postgresql" alt="PostgreSQL" />
  <img src="https://img.shields.io/badge/Bilingual-ID%20%F0%9F%87%AE%F0%9F%87%A9%20%7C%20EN%20%F0%9F%87%AC%F0%9F%87%A7-amber?style=for-the-badge" alt="Bilingual" />
</p>

<p align="center">
  <b>🌐 Live Frontend Website:</b> <a href="https://replate-supply.vercel.app" target="_blank">https://replate-supply.vercel.app</a><br/>
  <b>⚡ Live Backend API & Swagger:</b> <a href="https://replate.atsa.my.id/api/docs" target="_blank">https://replate.atsa.my.id/api/docs</a><br/>
  <b>📦 GitHub Monorepo:</b> <a href="https://github.com/keepleek/replate" target="_blank">https://github.com/keepleek/replate</a>
</p>

---

## 📌 Ringkasan Karya (Soedirman Technophoria 2026)

- **Bidang Kompetisi:** Web Development
- **Tema Utama:** *Byte-Sized Solutions for Global Food Security* (Ketahanan Pangan)
- **Sub Tema:** Sub Tema 1: *Food Waste & Supply Chain* (Manajemen Logistik & Penghematan)
- **Judul Karya:**  
  **REPLATE: Platform Rantai Pasok Surplus Pangan Berbasis *Food Safety Gate* Deterministik dan *Algorithmic Routing* untuk Menekan *Food Waste***

> **"Food should move. Not waste."**  
> *(Makanan harus bergerak, bukan terbuang.)*

**REPLATE** adalah platform manajemen dan penyelamatan surplus pangan cerdas (*Intelligent Food Surplus Routing & Upstream Prevention Platform*). Platform ini dirancang untuk menjembatani donor komersial sektor F&B (hotel, restoran, katering, bakery) dengan ekosistem penerima manfaat sosial (bank makanan, panti asuhan, dapur sosial) serta pengolah organik secara aman, transparan, dan terstandarisasi.

---

## 🛡️ Inovasi & Nilai Kebaruan Utama

1. **Food Safety Gate (Standar WHO, BPOM, Kemenkes RI):**
   - Gerbang penilai deterministik berbasis aturan sebelum makanan dapat diarahkan ke rute konsumsi manusia.
   - Menguji 6 parameter: Kategori Pangan, Suhu Penyimpanan (mitigasi *Danger Zone* 5°C–60°C), Integritas Kemasan (Cek KLIK BPOM), Riwayat Visual/Bau, Timestamp Masak (batas 4 jam Permenkes Jasaboga), dan Sisa Umur Simpan.
   - Menghasilkan status: `PASS` (konsumsi manusia), `REVIEW` (perlu kurasi staf), atau `REJECT` (dilarang konsumsi manusia).
2. **Hierarki Rute Penyelamatan (EPA / FAO Food Recovery Hierarchy):**
   - Makanan `PASS` diarahkan ke Konsumsi Manusia (`REDISTRIBUTE`).
   - Makanan non-PASS secara deterministik dialihkan ke Pengolahan Sekunder (`PROCESS`), Pakan Ternak (`ANIMAL_FEED`), Kompos Organik (`ORGANIC`), atau Pembuangan Aman (`SAFE_DISPOSAL`).
3. **Algorithmic Capacity Reservation & Anti-Overbooking:**
   - Transaksi database ACID dengan penguncian baris (`SELECT FOR UPDATE`) pada `RecipientCapacity` untuk mencegah overbooking kuota harian penerima dan *race condition*.
4. **Doorstep Physical Rejection:**
   - Hak konfirmasi akhir di tempat oleh penerima; pembatalan otomatis mengembalikan kuota harian penerima secara atomik dan tercatat pada `AuditLog`.
5. **SOS Emergency Distribution Hub:**
   - Siaran darurat pangan berbatas waktu (2–4 jam) untuk merespons krisis bencana atau kelaparan lokal dengan alokasi 1-klik donor.
6. **Model Dampak Lingkungan Ilmiah (ESG):**
   - Konversi reduksi emisi metana menggunakan model **US EPA WARM** ($2.5\text{ kg } CO_2e / \text{kg}$ pangan dialihkan dari TPA).
   - Standardisasi porsi makan merujuk patokan **FAO / GFN** ($0.35\text{ kg / porsi}$).
7. **Upstream Prevention Analytics:**
   - Membedah pola surplus harian dapur komersial untuk mengevaluasi dan mencegah *over-ordering* bahan baku di masa depan.

---

## 📁 Struktur Monorepo

```text
replate/
├── frontend/                     # Client Application (React 19 SPA)
│   ├── public/                   # Asset statis, logo, icon
│   ├── scripts/                  # Test suites (7 test suites)
│   ├── src/
│   │   ├── components/           # Komponen UI modular
│   │   ├── engine/               # Pure deterministic engines (Safety Gate, Route, Matching, Score)
│   │   ├── pages/                # Home, ReportSurplus, Assessment, Journey, SOSHub, Impact, dll.
│   │   ├── services/             # API client & local persistence (Tombstone isolation)
│   │   └── utils/                # i18n bilingual (ID/EN) & helpers
│   ├── package.json
│   ├── tailwind.config.js
│   └── vite.config.js
│
├── backend/                      # REST API Service (NestJS 10)
│   ├── prisma/
│   │   ├── schema.prisma         # Skema basis data 12 entitas relasional
│   │   ├── seed.ts               # Seeding master data & 9 akun Purbalingga
│   │   └── migrations/           # Riwayat migrasi SQL PostgreSQL
│   ├── src/
│   │   ├── common/               # Guards (JWT, Roles), Filters, Decorators, Utils (Haversine)
│   │   ├── config/               # Konfigurasi environment
│   │   └── modules/              # Auth, Surplus, Recipients, Journeys, Emergency, Analytics, Engines
│   ├── README.md                 # Dokumentasi backend NestJS
│   ├── package.json
│   └── tsconfig.json
│
├── .gitignore                    # Root gitignore
└── README.md                     # Master documentation
```

---

## 🚀 Panduan Menjalankan Aplikasi Secara Lokal

### Prasyarat
- Node.js versi 18 LTS atau lebih baru
- PostgreSQL 16 (atau Docker Desktop)
- Git & npm

---

### 1. Menjalankan Backend (NestJS API)

```bash
cd backend

# 1. Salin konfigurasi environment
cp .env.example .env

# 2. Pasang dependensi
npm install

# 3. Generate Prisma Client & jalankan migrasi database
npx prisma generate
npx prisma migrate dev

# 4. Masukkan master data & akun simulasi Purbalingga
npm run prisma:seed

# 5. Jalankan backend dalam mode development
npm run start:dev
```
Backend akan aktif di `http://localhost:3000` dan dokumentasi Swagger interaktif di `http://localhost:3000/api/docs`.

---

### 2. Menjalankan Frontend (React SPA)

```bash
cd frontend

# 1. Pasang dependensi
npm install

# 2. Jalankan aplikasi web lokal
npm run dev
```
Buka browser di `http://localhost:5173`. Frontend secara otomatis terhubung dengan API backend melalui dev proxy.

---

## 🧪 Pengujian & Jaminan Mutu (Quality Assurance)

### Frontend Test Suites (7 Berkas Pengujian — 100% PASS)
```bash
cd frontend
npm test
```
- `test-food-safety-gate.js`: 18 skenario evaluasi keamanan pangan (Danger zone, kondisi kemasan, expiry window).
- `test-rescue-performance.js`: 8 skenario analitik (Formula EPA WARM, porsi 0.35 kg, penanganan zero-division).
- `test-storage-demo-isolation.js`: 8 skenario isolasi data demo dan alur transisi status.
- `test-second-pass-audit.js`: 20 skenario matriks transisi 100 pasangan status dan imutabilitas status terminal.
- `test-workflow-role-fixes.js`: 9 skenario hak akses peran (RBAC).
- `test-tombstone-deletion.js`: 4 skenario proteksi penghapusan data (anti-resurrection).
- `test-sos-broadcast.js`: 6 skenario siaran darurat dan kedaluwarsa sinyal SOS.

### Backend Unit Tests
```bash
cd backend
npm test
```
Menguji kemurnian mesin *Food Safety Gate*, *Analytics Engine*, utilitas kalkulasi jarak spasial *Haversine*, dan *Role-Based Access Control Guards*.

---

## 👥 Akun Simulasi Pengujian (Demo Accounts Purbalingga)

Semua akun default menggunakan password: **`password123`**

| Peran | Nama Entitas | Email Akun | Deskripsi / Lokasi |
| :--- | :--- | :--- | :--- |
| **ADMIN** | BPBD & Bappeda Purbalingga | `admin@replate.id` | Pusat koordinasi & pengawasan kepatuhan wilayah |
| **SUPPLIER** | CV Surya Katering | `supplier@replate.id` | Donor F&B Purbalingga Kota (Alun-Alun) |
| **SUPPLIER** | Bakery Berkah Kalimanah | `supplier-kalimanah@replate.id` | Donor Roti & Pastry Kalimanah |
| **SUPPLIER** | Dapur Resto Bobotsari | `supplier-bobotsari@replate.id` | Donor Restoran Bobotsari |
| **SUPPLIER** | Resto Lembah Asri Karangreja | `supplier-karangreja@replate.id` | Donor Agrowisata Lereng Gn. Slamet |
| **MITRA** | Dapur Sosial Alun-Alun | `mitra@replate.id` | Penerima Pangan Purbalingga Kota |
| **MITRA** | Posko Pangan & Dapur Kalimanah | `purbalingga-kalimanah@replate.id` | Penerima Dapur Umum Kalimanah |
| **MITRA** | Bank Makanan Bobotsari | `purbalingga-bobotsari@replate.id` | Penerima Bank Makanan Bobotsari |
| **MITRA** | Posko Bencana Karangreja | `purbalingga-karangreja@replate.id` | Penerima Tanggap Darurat Bencana |

---

## 📄 Lisensi & Tim Pengembang
Dikembangkan untuk **Soedirman Technophoria (S-Tech) 2026** oleh Tim kiplik.  
Lisensi: MIT License.
