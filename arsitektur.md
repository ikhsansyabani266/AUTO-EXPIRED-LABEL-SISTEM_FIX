# Arsitektur Sistem

## 1. Gambaran Umum

AELS menggunakan pola **static multi-page frontend**. Setiap halaman HTML memuat library eksternal, client Supabase, shared logic, dan logic halaman masing-masing.

```text
Browser
  │
  ├── index.html ───────── dashboard.js
  ├── cetak-label.html ─── cetak-label.js
  ├── data-produk.html ─── data-produk.js
  ├── input-produk.html ── input-produk.js
  └── pengaturan.html ──── pengaturan.js
          │
          ├── shared.js
          ├── supabase-client.js
          ├── Tailwind CDN
          └── Supabase JS CDN
                    │
                    ▼
             Supabase REST/Realtime
                    │
                    ▼
              PostgreSQL Database
```

## 2. Lapisan Sistem

### Presentation Layer

Berisi file HTML, Tailwind utility class, dan `styles.css`. Halaman berbagi pola sidebar, top app bar, area konten, modal, dan print area.

### Page Logic Layer

Berisi file JavaScript berdasarkan halaman:

- `dashboard.js`
- `cetak-label.js`
- `data-produk.js`
- `input-produk.js`
- `pengaturan.js`

File ini mengatur event handler, render UI, validasi input, dan workflow halaman.

### Shared Layer

`shared.js` menyediakan state lokal, fungsi navigasi umum, status printer, toast, modal, dan helper yang dipakai lintas halaman.

### Data Access Layer

`supabase-client.js` menangani:

- Inisialisasi client Supabase.
- Sinkronisasi master product.
- Sinkronisasi riwayat produk.
- Sinkronisasi barista.
- Sinkronisasi pengaturan printer.
- Operasi insert, update, upsert, dan delete.
- Subscription realtime.

### Backend Configuration Layer

`api/config.js` adalah endpoint serverless yang mengirim `SUPABASE_URL` dan `SUPABASE_KEY` dari environment hosting ke frontend.

## 3. Alur Data Utama

### Inisialisasi Halaman

1. Browser memuat HTML.
2. CDN Tailwind, icon, font, dan Supabase dimuat.
3. `supabase-client.js` diinisialisasi.
4. Konfigurasi endpoint dicoba melalui `/api/config`.
5. Data awal disinkronkan dari Supabase.
6. Logic halaman mengisi komponen UI.
7. Subscription realtime memperbarui UI saat data berubah.

### Pembuatan Label

1. Pengguna memilih kategori dan produk.
2. Sistem mengambil masa simpan default dari master produk.
3. Pengguna mengisi tanggal buka dan data pendukung.
4. Sistem menghitung tanggal kedaluwarsa.
5. Data label disimpan ke `aels_products`.
6. Label dirender pada print area.
7. Browser atau service printer memproses pencetakan.
8. Counter total cetak diperbarui.

## 4. Model Data

```text
aels_master_products
- id: text, primary key
- name: text
- category: text
- days: integer

 aels_products
- id: text, primary key
- name: text
- category: text
- open_date: text
- shelf_life: integer
- expiry_date: text
- notes: text

 aels_baristas
- id: bigint, identity
- name: text, unique

 aels_print_settings
- id: integer, primary key
- printer_type: text
- printer_ip_address: text
- printer_port: text
- label_size: text
- total_printed: integer
```

## 5. Realtime

Supabase Realtime menggunakan perubahan PostgreSQL pada tabel aplikasi. Client mendaftarkan subscription dan memanggil refresh UI ketika tabel berubah.

## 6. Deployment

### Production

- Frontend dapat di-host sebagai static site.
- Folder `api` digunakan sebagai serverless function pada Vercel.
- Set `SUPABASE_URL` dan `SUPABASE_KEY` di environment variables.
- Jalankan SQL pada project Supabase production.

### Local

- Supabase CLI menggunakan `supabase/config.toml`.
- Docker Desktop atau Podman diperlukan.
- Jalankan stack lokal sebelum memakai perintah status/reset.

## 7. Batasan Arsitektur

- Tidak ada server aplikasi tradisional.
- State UI sebagian berada di browser.
- Keamanan data bergantung pada Supabase policies dan konfigurasi deployment.
- Printer jaringan tidak dikontrol langsung oleh database.

> Jangan mengubah ID elemen HTML atau nama tabel database tanpa memperbarui seluruh consumer terkait.