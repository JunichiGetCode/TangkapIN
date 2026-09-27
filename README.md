# Draf Isian Proposal PPL - TangkapIN (Versi Final)
*Gunakan teks dan tabel di bawah ini untuk mengisi bagian-bagian yang kosong (<...>) di dalam file Word Anda.*

---

## 1. Usulan Solusi
**Jelaskan solusi permasalahan yang ada di latar belakang dengan produk web atau Sistem Informasi yang diusulkan:**
Solusi yang diusulkan adalah **TangkapIN**, sebuah sistem informasi *Single Page Application* (SPA) yang mengintegrasikan kapabilitas dasbor analitik data dengan fungsionalitas *e-commerce* (*marketplace*). Sistem ini menengahi dua masalah sekaligus: meminimalisir praktik penangkapan ikan berlebih (*overfishing*) dengan memberikan wawasan (*insight*) tren kelimpahan ikan kepada nelayan, serta mencegah kerugian finansial akibat ikan membusuk melalui ketersediaan etalase publik yang dikelola secara terpusat oleh Admin.

**Jelaskan keterkaitan permasalahan dengan solusi yang diusulkan:**
Permasalahan nelayan yang menangkap ikan secara buta (berdasarkan insting) diselesaikan melalui fitur *Dashboard Analitik* yang menyajikan grafik tren data yang diolah secara *native* oleh sistem. Sementara itu, masalah distribusi ikan yang terputus diselesaikan melalui fitur *Marketplace* yang memfasilitasi penjualan langsung ke pelanggan dengan sistem pembayaran otomatis (Midtrans). Hal ini secara langsung mendukung **SDG 14 (Life Below Water)** dan peningkatan ekonomi pesisir.

---

## 2. Deskripsi Produk
TangkapIN adalah platform web modern yang memisahkan beban kerja antara nelayan (fokus ke laut) dan tim manajemen (Admin yang fokus jualan). 
**Fungsi Utama:**
1. **Pencatatan & Analitik Terpusat:** Admin mencatat hasil panen harian nelayan yang kemudian dikomputasi secara efisien menggunakan logika agregasi *database* (Eloquent ORM) untuk menampilkan grafik tren kepada nelayan.
2. **Manajemen Etalase Terpusat:** Admin dapat mengonversi data panen tersebut menjadi stok produk yang siap dijual di etalase publik.
3. **Transaksi Cerdas:** Pembeli (Customer) dapat berbelanja hasil laut secara *real-time* dengan metode pembayaran otomatis yang ditangani oleh Midtrans Payment Gateway.

**Keunggulan Produk:** 
Penerapan arsitektur VILT Stack (Vue.js, Inertia, Laravel, Tailwind) dipadukan dengan *database* PostgreSQL. Hal ini menjamin aplikasi berjalan sangat cepat, tanpa *loading* ulang halaman (responsif layaknya aplikasi *mobile*), dan mampu memproses agregasi analitik data dalam jumlah besar.

---

## 3. Proses Bisnis
**Proses Bisnis Existing (Sebelum ada sistem):**
1. Nelayan melaut dan menangkap ikan berdasarkan perkiraan atau musim semata.
2. Setelah berlabuh, nelayan hanya menjualnya ke tengkulak lokal dengan harga sepihak.
3. Sisa ikan yang tidak dibeli tengkulak rentan membusuk karena tidak adanya akses ke pasar yang lebih luas.
4. Pembeli akhir harus melewati rantai pasok yang sangat panjang untuk mendapatkan ikan segar.

**Proses Bisnis Usulan (Setelah ada TangkapIN):**
1. Admin TangkapIN memasukkan data panen harian (spesies, berat) dari nelayan ke dalam sistem.
2. Sistem mengolah data tersebut menjadi grafik wawasan yang dapat dipantau oleh Nelayan melalui dasbor mereka.
3. Admin menyeleksi hasil tangkapan, mengatur harga jual, dan mempublikasikannya ke katalog *Marketplace*.
4. Pembeli (Customer) membuka web TangkapIN, memilih ikan, memasukkan ke keranjang, dan melakukan *checkout*.
5. Pembeli membayar pesanan melalui Midtrans Gateway, status pesanan otomatis lunas, dan sistem memberikan instruksi kepada Admin untuk menyiapkan pengiriman logistik.

---

## 4. Kebutuhan Sistem
### Kebutuhan Fungsional
| ID | Kebutuhan Fungsional | Deskripsi |
| :--- | :--- | :--- |
| FR-01 | Manajemen Data Panen | Admin dapat menambah, melihat, mengubah, dan menghapus data hasil tangkapan nelayan (spesies, berat, tanggal, nama nelayan penginput) sebagai bahan dasar analitik. |
| FR-02 | Manajemen Etalase & Katalog | Admin menyeleksi hasil tangkapan yang melimpah, menentukan harga jual, dan mempublikasikannya sebagai produk ke etalase publik. |
| FR-03 | Manajemen Transaksi & Logistik | Admin memantau pesanan yang masuk dari Customer, memperbarui status pengiriman, dan menugaskan alur logistik setelah sistem menerima webhook Midtrans bahwa pembayaran lunas. |
| FR-04 | Dashboard Evaluasi Ekonomi | Admin memantau grafik rekapitulasi yang membandingkan total volume panen dengan volume penjualan guna menilai dampak aplikasi terhadap ekonomi nelayan. |
| FR-05 | Kelola Master Data & Pengguna | Admin mengontrol referensi kategori spesies ikan serta melakukan moderasi terhadap seluruh pengguna (menambah/memblokir Nelayan dan Customer). |
| FR-06 | Dashboard Analitik Nelayan | Nelayan dapat melihat visualisasi tren kelimpahan hasil tangkapan (filter harian, mingguan, bulanan, tahunan) beserta rincian pendapatan dari tangkapan yang telah berhasil dijual oleh Admin. |
| FR-07 | Portal E-Commerce Customer | Customer dapat menelusuri katalog real-time, menambahkan produk ke keranjang, melakukan checkout via Snap Window Midtrans Sandbox, dan memantau status pesanannya secara mandiri. |

### Karakteristik Pengguna
| Pengguna | Tanggung Jawab | Hak Akses / Tingkat Keahlian |
| :--- | :--- | :--- |
| **Admin** | Mengelola seluruh data panen, etalase & harga, transaksi & logistik, evaluasi dampak ekonomi, serta master data dan moderasi pengguna. | Akses penuh ke seluruh modul sistem (full CRUD). Membutuhkan pemahaman dasar tentang operasional platform dan interpretasi data analitik. |
| **Nelayan** | Memantau dashboard analitik tren tangkapan dan rekap pendapatan hasil penjualan yang dikelola Admin. | Akses baca (read-only) hanya pada dashboard pribadi. Tidak memerlukan keahlian teknis khusus — cukup familiar dengan penggunaan aplikasi web/mobile dasar. |
| **Customer** | Menelusuri katalog, melakukan pemesanan, checkout, dan memantau status transaksi secara mandiri. | Akses baca & tulis terbatas pada modul e-commerce (katalog, keranjang, checkout, riwayat pesanan). Pengguna umum, tidak memerlukan keahlian teknis. |

### Kebutuhan Non Fungsional
| ID | Kebutuhan Non Fungsional | Deskripsi |
| :--- | :--- | :--- |
| NFR-01 | UI Consistency | Seluruh navigasi/navbar dan tombol profil pengguna wajib seragam secara ukuran dan tipografi (tanpa ikon dekoratif). |
| NFR-02 | Performance | Waktu muat (*load time*) untuk perpindahan halaman (*routing*) dan rendering grafik agregasi data tidak boleh melebihi 3 detik. |
| NFR-03 | Security | Jalur komunikasi antara web dan API Midtrans wajib dilindungi dan diverifikasi menggunakan parameter *Signature Key* untuk mencegah manipulasi pembayaran. |

### Kebutuhan Teknis
| ID | Kebutuhan Teknis | Deskripsi |
| :--- | :--- | :--- |
| TR-01 | Framework Frontend & Backend | Menggunakan VILT Stack (Vue.js, Inertia.js, Laravel, Tailwind CSS) untuk membangun *Single Page Application* (SPA). |
| TR-02 | Basis Data (RDBMS) | Menggunakan PostgreSQL (terkonfigurasi pada port 5432) untuk menunjang keamanan dan keandalan query agregasi data berskala besar. |
| TR-03 | API / Payment Gateway | Membutuhkan integrasi API dari Midtrans (*Sandbox Mode*) untuk layanan dan simulasi transaksi pembayaran. |

---

## 5. Metode Pengembangan
Pengembangan TangkapIN menggunakan metodologi **Agile (Scrum)**.

## 6. Jadwal Pengembangan
*(Berdasarkan tiket pada proyek Jira, waktu pengembangan dibagi menjadi 5 Sprint utama)*:
1. **Sprint 1:** Penyusunan Proposal Proyek Perangkat Lunak.
2. **Sprint 2:** Infrastruktur Dasar, Basis Data & UI Inti.
3. **Sprint 3:** Manajemen Tangkapan & Dashboard Analitik.
4. **Sprint 4:** Etalase Marketplace & Manajemen E-Commerce.
5. **Sprint 5:** Gateway Pembayaran (Midtrans), Laporan, & Pengujian.