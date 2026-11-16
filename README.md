# AELS — Auto Expired Label Sistem

> Sistem manajemen label kedaluwarsa untuk membantu operasional coffee shop mengelola masa simpan produk, mencetak label, dan memantau riwayat pelabelan.

<div align="center">

![AELS Logo](logo-aels.svg)

**Auto Expired Label Sistem**  
Aplikasi operasional untuk pencatatan masa simpan dan pencetakan label produk.

</div>

---

## 📌 Informasi Project

| Informasi | Detail |
|---|---|
| Nama Project | Auto Expired Label Sistem (AELS) |
| Jenis Aplikasi | Frontend web multi-page |
| Pengembang | Muhamad Ikhsan Syabani |
| Target Pengguna | Barista, staf operasional, supervisor, dan admin coffee shop |
| Database | Supabase PostgreSQL |
| Deployment | Vercel atau static hosting |
| Status | Aktif dikembangkan |

## ✨ Deskripsi Project

AELS adalah aplikasi internal yang membantu coffee shop mengelola masa simpan produk dengan lebih teratur. Sistem ini menghitung tanggal kedaluwarsa berdasarkan tanggal buka dan masa simpan, menyimpan riwayat pelabelan, serta mendukung pencetakan label melalui printer thermal.

Aplikasi menggunakan Supabase untuk penyimpanan data dan sinkronisasi realtime antar tab atau perangkat yang terhubung.

## 🎯 Tujuan

- Mengurangi kesalahan dalam menghitung tanggal kedaluwarsa.
- Menstandarkan format label produk.
- Mempercepat proses input dan cetak label.
- Menyediakan riwayat produk yang mudah dicari dan dikelola.
- Menyinkronkan data master produk, barista, dan pengaturan printer.

## 🚀 Fitur Utama

### Dashboard

- Melihat ringkasan produk aktif.
- Memantau produk yang mendekati kedaluwarsa.
- Memantau produk yang sudah kedaluwarsa.
- Melihat status printer dan total label tercetak.

### Cetak Label

- Memilih kategori dan produk.
- Mengisi tanggal buka produk.
- Menggunakan masa simpan dari master SOP.
- Menghitung tanggal kedaluwarsa secara otomatis.
- Menyimpan catatan dan nama barista.
- Mencetak atau mencetak ulang label.

### Data Produk

- Melihat riwayat pelabelan.
- Mengedit data produk.
- Menghapus data produk.
- Mereset riwayat sesuai kebutuhan operasional.

### Input Produk

- Menambah master produk.
- Mengatur kategori produk.
- Mengatur masa simpan default.
- Memperbarui data SOP produk.

### Pengaturan

- Mengelola daftar barista.
- Mengatur tipe printer.
- Mengatur alamat IP dan port printer jaringan.
- Mengatur ukuran label.
- Melihat dan mengelola konfigurasi aplikasi.

## 🧰 Teknologi yang Digunakan

- **HTML5** — struktur halaman.
- **JavaScript ES6+** — logika aplikasi dan interaksi pengguna.
- **Tailwind CSS** — utility styling melalui CDN.
- **CSS** — animasi, modal, scrollbar, dan layout print thermal.
- **Font Awesome** — ikon antarmuka.
- **Google Fonts** — Plus Jakarta Sans dan Share Tech Mono.
- **Supabase PostgreSQL** — database aplikasi.
- **Supabase Realtime** — sinkronisasi perubahan data.
- **Vercel Serverless Function** — endpoint konfigurasi environment.

## 📁 Struktur Project

```text
AUTO EXPIRED LABEL SISTEM/
├── api/
│   └── config.js              # Endpoint konfigurasi Supabase
├── supabase/
│   ├── config.toml            # Konfigurasi Supabase lokal
│   └── .gitignore             # File lokal Supabase yang diabaikan Git
├── index.html                 # Dashboard
├── cetak-label.html           # Halaman cetak label
├── data-produk.html           # Riwayat data produk
├── input-produk.html          # Master SOP produk
├── pengaturan.html            # Pengaturan aplikasi
├── dashboard.js               # Logic dashboard
├── cetak-label.js             # Logic pencetakan label
├── data-produk.js             # Logic riwayat produk
├── input-produk.js             # Logic master produk
├── pengaturan.js              # Logic pengaturan
├── shared.js                  # Helper dan state bersama
├── supabase-client.js         # Client database Supabase
├── styles.css                 # CSS tambahan dan aturan print
├── tailwind-config.js         # Konfigurasi Tailwind
├── setup.sql                  # Schema database Supabase
├── logo-aels.svg              # Logo aplikasi
├── prd.md                     # Product Requirements Document
├── tech-stack.md              # Dokumentasi teknologi
├── arsitektur.md              # Dokumentasi arsitektur sistem
├── ui.ux.md                   # Panduan UI/UX
├── instruction.md             # Panduan developer
├── .gitignore                 # Aturan file yang diabaikan Git
└── README.md                  # Dokumentasi repository
```

## ⚙️ Persiapan

Pastikan perangkat sudah memiliki:

- Git.
- Browser modern seperti Chrome, Edge, atau Firefox.
- Python 3 atau static web server lain.
- Project Supabase jika fitur database digunakan.
- Docker Desktop atau Podman untuk Supabase lokal.

## ▶️ Menjalankan Secara Lokal

Buka PowerShell pada folder project, lalu jalankan:

```powershell
python -m http.server 8000
```

Buka:

```text
http://localhost:8000/index.html
```

Menjalankan melalui HTTP server lebih disarankan daripada membuka file melalui `file://`, khususnya saat menguji endpoint API dan sinkronisasi data.

## 🗄️ Konfigurasi Supabase

1. Buat atau pilih project pada Supabase.
2. Buka menu **SQL Editor**.
3. Jalankan seluruh isi file `setup.sql`.
4. Pastikan tabel berikut tersedia:
   - `aels_master_products`
   - `aels_products`
   - `aels_baristas`
   - `aels_print_settings`
5. Pastikan konfigurasi Realtime sesuai kebutuhan project.

### Environment Variable

Untuk deployment dengan endpoint `api/config.js`, gunakan:

```text
SUPABASE_URL=your_supabase_project_url
SUPABASE_KEY=your_supabase_anon_key
```

Jangan commit file `.env`, password, service role key, atau credential private ke repository.

## ☁️ Deployment ke Vercel

1. Push repository ke GitHub.
2. Import repository pada Vercel.
3. Tambahkan environment variable `SUPABASE_URL`.
4. Tambahkan environment variable `SUPABASE_KEY`.
5. Deploy project.
6. Buka URL deployment dan uji seluruh halaman.
7. Pastikan fitur database, realtime, dan pencetakan berjalan sesuai lingkungan deployment.

Folder `api` akan diperlakukan sebagai serverless function oleh Vercel.

## 🖨️ Konfigurasi Printer

AELS mendukung workflow browser dan printer jaringan sesuai konfigurasi aplikasi.

Untuk printer jaringan, siapkan:

- Alamat IP printer.
- Port printer, biasanya `9100` jika sesuai perangkat.
- Ukuran label yang digunakan.
- Service print lokal jika diperlukan oleh lingkungan printer.

Pastikan browser dan printer berada pada jaringan yang dapat saling mengakses.

## 🧪 Validasi dan Testing

Pemeriksaan syntax seluruh JavaScript:

```powershell
Get-ChildItem -File -Filter '*.js' | ForEach-Object {
    node.exe --check $_.FullName
}
```

Pemeriksaan format perubahan Git:

```powershell
git diff --check
```

Pemeriksaan status repository:

```powershell
git status --short
```

Pengujian manual minimum:

- Buka dashboard.
- Uji navigasi seluruh menu.
- Tambahkan master produk.
- Buat label baru.
- Pastikan tanggal kedaluwarsa benar.
- Simpan dan cetak label.
- Periksa riwayat produk.
- Uji pengaturan barista dan printer.
- Uji tampilan desktop dan mobile.

## 🔐 Catatan Keamanan

- Jangan menyimpan service role key pada frontend.
- Jangan commit file `.env` atau credential private.
- Tinjau Row Level Security sebelum aplikasi digunakan publik.
- Validasi input sebelum menyimpan data.
- Batasi akses database sesuai kebutuhan pengguna.
- Jangan menampilkan secret pada log atau dokumentasi.

> Konfigurasi database saat ini ditujukan untuk penggunaan internal. Tinjau policy dan autentikasi sebelum deployment publik.

## 📚 Dokumentasi Tambahan

- [`prd.md`](prd.md) — kebutuhan dan ruang lingkup produk.
- [`tech-stack.md`](tech-stack.md) — teknologi dan konvensi teknis.
- [`arsitektur.md`](arsitektur.md) — arsitektur dan alur data.
- [`ui.ux.md`](ui.ux.md) — pedoman antarmuka dan pengalaman pengguna.
- [`instruction.md`](instruction.md) — panduan development, testing, dan deployment.
- [`setup.sql`](setup.sql) — schema database Supabase.

## 👨‍💻 Pengembang

**Muhamad Ikhsan Syabani**  
Project AELS — Auto Expired Label Sistem

## 📄 Lisensi

Belum ditentukan. Tambahkan lisensi resmi sebelum project didistribusikan secara publik.

---

⭐ Jika repository ini membantu proses pengembangan atau dokumentasi project, silakan berikan star pada repository GitHub.

