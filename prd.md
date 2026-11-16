# Product Requirements Document (PRD)

## 1. Ringkasan Produk

**AELS (Auto Expired Label Sistem)** adalah aplikasi internal untuk membantu coffee shop mengelola masa simpan produk, mencetak label kedaluwarsa, dan memantau riwayat pelabelan secara terpusat.

## 2. Masalah yang Diselesaikan

- Pencatatan tanggal kedaluwarsa masih rawan kesalahan manual.
- Informasi masa simpan produk perlu tersedia secara konsisten.
- Proses cetak label perlu lebih cepat dan terstandar.
- Data produk dan pengaturan printer perlu dapat digunakan dari beberapa halaman/perangkat.

## 3. Target Pengguna

- Barista dan staf operasional coffee shop.
- Supervisor atau pemilik usaha.
- Admin yang mengelola master produk dan pengaturan printer.

## 4. Tujuan Produk

- Menghitung tanggal kedaluwarsa berdasarkan tanggal buka dan masa simpan.
- Membantu staf mencetak label produk secara konsisten.
- Menyediakan dashboard status produk aktif, mendekati kedaluwarsa, dan kedaluwarsa.
- Menyimpan master SOP produk, daftar barista, riwayat produk, dan pengaturan printer.

## 5. Fitur Utama

### Dashboard

- Menampilkan ringkasan status produk.
- Menampilkan daftar produk yang perlu diperhatikan.
- Menampilkan status koneksi printer dan total label tercetak.

### Cetak Label

- Memilih kategori dan produk.
- Mengisi tanggal buka, barista, catatan, dan masa simpan.
- Menghitung tanggal kedaluwarsa otomatis.
- Mencetak label dan mendukung proses cetak ulang.

### Data Produk

- Melihat riwayat pelabelan.
- Mengedit, menghapus, dan mereset data produk sesuai hak operasional aplikasi.

### Input Produk

- Menambah dan memperbarui master SOP produk.
- Mengatur kategori dan masa simpan default.

### Pengaturan

- Mengelola daftar barista.
- Mengatur tipe printer, alamat IP, port, dan ukuran label.
- Mengelola data cloud dan melakukan reset sesuai kebutuhan operasional.

## 6. Kriteria Keberhasilan

- Staf dapat membuat label tanpa menghitung tanggal secara manual.
- Data label tersimpan dan dapat ditampilkan kembali.
- Perubahan data dapat tersinkronisasi melalui Supabase Realtime.
- Halaman dapat digunakan pada desktop maupun perangkat mobile.
- Label tercetak dengan format yang sesuai printer thermal.

## 7. Batasan dan Catatan

- Aplikasi saat ini ditujukan untuk penggunaan internal.
- Autentikasi pengguna belum menjadi bagian dari workflow saat ini.
- Koneksi printer jaringan bergantung pada konfigurasi jaringan lokal.
- Library frontend dimuat melalui CDN.
- Variabel Supabase untuk deployment sebaiknya disimpan sebagai environment variable di platform hosting.

## 8. Di Luar Ruang Lingkup Saat Ini

- Sistem kasir atau inventori lengkap.
- Manajemen akun dan role pengguna.
- Notifikasi email atau WhatsApp otomatis.
- Aplikasi native Android/iOS.
- Integrasi langsung dengan sistem POS eksternal.

## 9. Prioritas Pengembangan Berikutnya

1. Menambahkan autentikasi dan role-based access.
2. Menambahkan validasi keamanan dan Row Level Security Supabase.
3. Menambahkan pengujian otomatis untuk kalkulasi tanggal dan operasi data.
4. Menambahkan audit log untuk perubahan data penting.
5. Menambahkan observability dan penanganan error yang lebih terstruktur.

---

**Status dokumen:** Baseline proyek saat ini  
**Nama produk:** Auto Expired Label Sistem (AELS)

### Referensi

- `index.html`
- `cetak-label.html`
- `data-produk.html`
- `input-produk.html`
- `pengaturan.html`
- `setup.sql`

> Catatan: Dokumen ini menggambarkan perilaku aplikasi yang ada dan tidak mengubah workflow implementasi.