# Dokumen Persyaratan Produk (PRD)
**Nama Proyek:** TangkapIN (Sistem Analitik & Marketplace Hasil Laut)
**Kategori:** Proyek Perangkat Lunak S1 Sistem Informasi
**Versi:** 5.0 (Penyederhanaan Arsitektur Native VILT & Hak Akses Baru)

---

## 1. Ringkasan Eksekutif & Latar Belakang Masalah
Industri perikanan skala kecil sering kali menghadapi dua masalah utama: rantai pasok yang panjang yang merugikan nelayan, dan kurangnya wawasan data yang memicu praktik penangkapan ikan berlebih (*overfishing*). 

**TangkapIN** hadir sebagai solusi sistem informasi *full-stack* inovatif yang memadukan kapabilitas **analitik data terpusat** dengan **fungsionalitas e-niaga (marketplace)**. Objektif utama dari sistem ini adalah memutus siklus *overfishing* dengan memberikan wawasan (*insights*) berbasis data kepada nelayan mengenai tren tangkapan laut. Di saat yang sama, sistem ini secara langsung menekan angka kerugian finansial akibat ikan tangkapan yang membusuk atau tidak terjual, melalui fitur marketplace terintegrasi B2B/B2C.

## 2. Metodologi Pengembangan
Sistem ini dikembangkan menggunakan metodologi **Agile (Scrum)**.

## 3. Spesifikasi Arsitektur & Teknologi (*Tech Stack*)
*   **Lingkungan Lokal:** Visual Studio Code (IDE), Laragon / XAMPP (Local Web Server).
*   **Kerangka Kerja (VILT Stack):** Vue.js, Inertia.js, Laravel (PHP), Tailwind CSS.
*   **Visualisasi Data:** Menggunakan *library* JavaScript modern seperti **Chart.js** atau **ApexCharts**.
*   **Basis Data (RDBMS):** PostgreSQL.
*   **Integrasi Pihak Ketiga (Fintech):** Midtrans Payment Gateway (Mode *Sandbox*).

## 4. Kebutuhan Fungsional (*User Stories & Roles*)
*(Catatan: Nelayan bersifat Read-Only untuk analitik, sementara Admin memegang kendali CRUD data panen & etalase).*

### 4.1 Peran: Admin (Tim TangkapIN)
*   **Manajemen Data Panen:** Admin mencatat, melihat, mengubah, dan menghapus data panen harian nelayan.
*   **Manajemen Etalase:** Admin menyeleksi hasil tangkapan dan mempublikasikannya ke etalase publik.
*   **Kontrol Pesanan & Logistik:** Memantau pesanan masuk dan mengatur pengiriman saat pembayaran lunas.
*   **Laporan Evaluasi:** Memantau komparasi total panen vs total penjualan.
*   **Kelola Master Data:** Memoderasi pengguna dan referensi spesies ikan.

### 4.2 Peran: Nelayan
*   **Dashboard Analitik:** Nelayan memantau dasbor cerdas berisi grafik tren tangkapan dan rekapitulasi penjualan untuk panduan melaut berikutnya.

### 4.3 Peran: Customer (Pembeli B2B/B2C)
*   **Katalog & Keranjang:** Eksplorasi stok hasil laut, pencarian, dan penambahan item ke keranjang.
*   **Transaksi & Pembayaran:** Melakukan *checkout* melalui layar terintegrasi *Snap Window Midtrans*.

## 5. Skema Basis Data (Data Dictionary)
| Tabel | Kolom | Tipe Data | Relasi / Keterangan |
| :--- | :--- | :--- | :--- |
| users | id, name, email, password, role | PK, String, String, Hash, Enum | role: 'nelayan', 'customer', 'admin' |
| catch_records | id, user_id, species, weight_kg, date | PK, FK, String, Float, Date | FK ke users.id (nelayan) |
| products | id, catch_id, price_kg, stock, status | PK, FK, Decimal, Float, Boolean | FK ke catch_records.id |
| orders | id, buyer_id, total, status, snap_token | PK, FK, Decimal, Enum, String | |
| order_items | id, order_id, product_id, qty, subtotal | PK, FK, FK, Float, Decimal | |
| payments | id, order_id, method, status, payload | PK, FK, String, Enum, JSON | Rekam jejak *webhook* Midtrans |

## 6. Jadwal Eksekusi 5 Sprint
*   **Sprint 1:** Penyusunan Proposal Proyek Perangkat Lunak.
*   **Sprint 2:** Infrastruktur Dasar, Basis Data & UI Inti.
*   **Sprint 3:** Manajemen Tangkapan & Dashboard Analitik.
*   **Sprint 4:** Etalase Marketplace & Manajemen E-Commerce.
*   **Sprint 5:** Gateway Pembayaran (Midtrans), Laporan, & Pengujian.