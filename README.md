# Dokumen Persyaratan Produk (PRD)
**Nama Proyek:** TangkapIN (Sistem Analitik & Marketplace Hasil Laut)
**Kategori:** Proyek Proyek Perangkat Lunak S1 Sistem Informasi
**Versi:** 5.0 (Penyederhanaan Arsitektur Native VILT)

---

## 1. Ringkasan Eksekutif & Latar Belakang Masalah
Industri perikanan skala kecil sering kali menghadapi dua masalah utama: rantai pasok yang panjang yang merugikan nelayan, dan kurangnya wawasan data yang memicu praktik penangkapan ikan berlebih (*overfishing*). 

**TangkapIN** hadir sebagai solusi sistem informasi *full-stack* inovatif yang memadukan kapabilitas **analitik data terpusat** dengan **fungsionalitas e-niaga (marketplace)**. Objektif utama dari sistem ini adalah memutus siklus *overfishing* dengan memberikan wawasan (*insights*) berbasis data kepada nelayan mengenai tren tangkapan laut. Di saat yang sama, sistem ini secara langsung menekan angka kerugian finansial akibat ikan tangkapan yang membusuk atau tidak terjual, melalui fitur marketplace terintegrasi B2B/B2C.

## 2. Metodologi Pengembangan
Sistem ini dikembangkan menggunakan metodologi **Agile (Scrum)**.

## 3. Spesifikasi Arsitektur & Teknologi (*Tech Stack*)
Pengembangan dibagi menjadi lapisan arsitektur modular yang memisahkan logika bisnis dan antarmuka.
*   **Lingkungan Lokal:** Visual Studio Code (IDE), Laragon / XAMPP (Local Web Server).
*   **Kerangka Kerja (VILT Stack):** 
    *   **Vue.js & Tailwind CSS:** Untuk antarmuka pengguna (Frontend) yang reaktif (*Single Page Application*) dan *styling* yang modern.
    *   **Inertia.js:** Sebagai penghubung *seamless* antara Frontend dan Backend tanpa perlu membangun REST API secara terpisah.
    *   **Laravel (PHP):** Sebagai mesin utama Backend untuk *routing*, logika agregasi data cerdas, dan manajemen basis data menggunakan Eloquent ORM.
*   **Visualisasi Data (Frontend):** Menggunakan *library* JavaScript modern seperti **Chart.js** atau **ApexCharts** untuk merender grafik interaktif di Dasbor.
*   **Basis Data (RDBMS):** PostgreSQL.
*   **Integrasi Pihak Ketiga (Fintech):** Midtrans Payment Gateway (Mode *Sandbox* untuk simulasi transaksi).

## 4. Kebutuhan Fungsional (*User Stories*)
### 4.1 Peran: Nelayan
*Fokus: Suplai data hasil laut dan analisis panen.*
*   **Pencatatan Data Panen:** Sistem menerima input data panen (spesies, berat, tanggal) dan merekamnya dalam catch_records.
*   **Dashboard Analitik & Pendapatan:** Sistem menampilkan dasbor cerdas berisi grafik tren tangkapan dengan filter dinamis. *(Catatan: Nelayan tidak berinteraksi dengan proses penjualan secara langsung).*

### 4.2 Peran: Customer (Pembeli B2B/B2C)
*Fokus: Penjelajahan katalog, transaksi, dan dukungan ekonomi sirkular.*
*   **Katalog & Keranjang Belanja:** Eksplorasi ketersediaan stok hasil laut *real-time*, fungsi pencarian canggih, dan penambahan item ke keranjang.
*   **Transaksi & Pembayaran:** Integrasi mulus dengan *API Midtrans*.
*   **Pembaruan Pesanan Otomatis:** Sistem mendengarkan *Signature Key* dari Webhook Midtrans.

### 4.3 Peran: Admin (Tim TangkapIN)
*Fokus: Manajemen penjualan, pengawasan integritas sistem, kendali platform, dan evaluasi ekonomi.*
*   **Manajemen Etalase (Marketplace):** Admin memverifikasi data panen dari nelayan, mengatur harga jual, dan mempublikasikan stok ikan ke etalase publik.
*   **Kontrol Aktivitas Web & Pesanan:** Akses otoritas penuh untuk memantau transaksi dan mengelola alur produk.
*   **Rekapitulasi Evaluasi (Laporan Proyek Perangkat Lunak):** Laporan komparatif antara total volume panen vs volume penjualan.

## 5. Pedoman Tata Letak & Antarmuka (*UI/UX Guidelines*)
*   **Sistem Navigasi Utama (Navbar):** Seluruh elemen dalam navbar **wajib** memiliki dimensi seragam.
*   **Elemen Profil Pengguna:** Tombol aksi pada area *header* khusus profil dirancang secara minimalis **hanya menggunakan teks** (tanpa ikon dekoratif).

## 6. Skema Basis Data Lanjutan (*Data Dictionary*)
| Tabel | Kolom | Tipe Data | Relasi / Keterangan |
| :--- | :--- | :--- | :--- |
| users | id, name, email, password, role | PK, String, String, Hash, Enum | role: 'nelayan', 'customer', 'admin' |
| catch_records | id, user_id, species, weight_kg, date | PK, FK, String, Float, Date | FK ke users.id |
| products | id, catch_id, price_kg, stock, status | PK, FK, Decimal, Float, Boolean | FK ke catch_records.id |
| orders | id, buyer_id, total, status, snap_token | PK, FK, Decimal, Enum, String | Token akses Midtrans |
| order_items | id, order_id, product_id, qty, subtotal | PK, FK, FK, Float, Decimal | Relasi Many-to-Many pesanan |
| payments | id, order_id, method, status, payload | PK, FK, String, Enum, JSON | Rekam jejak *callback* Midtrans |

## 7. Jadwal Eksekusi 5 Sprint (*Sprint Backlog*)
### Sprint 1: Penyusunan Proposal Proyek Perangkat Lunak
*   Melengkapi dokumen proposal Bab 1 hingga Bab 4.

### Sprint 2: Infrastruktur Dasar, Basis Data & UI Inti
*   Instalasi & Konfigurasi *Environment* VILT Stack menggunakan Laravel Breeze di Laragon.
*   Penyusunan file *Migration*, *Model*, dan *Controller* dasar.
*   Penetapan *Role-Based Access Control (RBAC)* melalui fitur *Middleware* Laravel.
*   Implementasi kerangka antarmuka utama berbasis Tailwind & Vue.

### Sprint 3: Manajemen Tangkapan & Dashboard Analitik
*   Pengembangan formulir input dan manajemen rekaman tangkapan ikan untuk panel Nelayan.
*   Pembuatan logika query agregasi data panen menggunakan Laravel Eloquent ORM.
*   Integrasi *library* grafik (Chart.js/ApexCharts) ke Dashboard Nelayan untuk visualisasi tren.
*   Pembuatan kalkulator otomatis untuk proyeksi pendapatan nelayan di halaman dasbor.

### Sprint 4: Etalase Marketplace & Manajemen E-Commerce
*   Pengembangan fitur Manajemen Produk bagi Admin untuk mengkonversi data tangkapan menjadi produk siap jual.
*   Desain dan implementasi antarmuka etalase produk publik untuk *Customer*.
*   Pembuatan logika *Keranjang Belanja* (Cart) dan manajemen sesi pesanan.
*   Penyusunan *Dashboard Panel Admin* untuk memonitor ketersediaan produk, mengatur harga, dan pemesanan.

### Sprint 5: Gateway Pembayaran (Midtrans), Laporan, & Pengujian
*   Koneksi sistem *Checkout* dengan kredensial API Midtrans (*Sandbox Mode*).
*   Pembuatan rute *Webhook/Callback* yang aman untuk perubahan status pembayaran.
*   Pengembangan fitur "Laporan Rekapitulasi Evaluasi Ekonomi" pada Panel Admin.
*   Pengujian fungsionalitas keseluruhan aplikasi (*End-to-End Testing*).
