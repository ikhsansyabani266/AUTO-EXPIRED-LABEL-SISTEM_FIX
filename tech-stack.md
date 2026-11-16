# Technical Stack

## 1. Ringkasan

AELS menggunakan arsitektur frontend statis dengan JavaScript vanilla dan Supabase sebagai backend-as-a-service.

## 2. Teknologi Utama

| Area | Teknologi | Penggunaan |
|---|---|---|
| Markup | HTML5 | Struktur halaman aplikasi |
| Bahasa pemrograman | JavaScript ES6+ | Interaksi UI, kalkulasi, state, dan operasi data |
| Styling | Tailwind CSS CDN | Utility styling pada halaman |
| Styling tambahan | CSS | Animasi, scrollbar, modal, dan print thermal |
| Icon | Font Awesome 6.4.0 CDN | Ikon navigasi dan kontrol UI |
| Font | Google Fonts | Plus Jakarta Sans dan Share Tech Mono |
| Database | Supabase PostgreSQL | Penyimpanan data aplikasi |
| Realtime | Supabase Realtime | Sinkronisasi perubahan data antar tab/perangkat |
| Client database | `@supabase/supabase-js` 2.45.4 | Akses Supabase dari browser |
| API config | Vercel Serverless Function | Menyediakan konfigurasi environment ke frontend |
| Local development | Supabase CLI + Docker/Podman | Menjalankan stack Supabase lokal |
| Deployment | Vercel atau static hosting | Hosting frontend dan endpoint API |

## 3. Struktur File Utama

```text
/
├── index.html              # Dashboard
├── cetak-label.html        # Form dan halaman cetak label
├── data-produk.html        # Riwayat produk
├── input-produk.html       # Master SOP produk
├── pengaturan.html         # Pengaturan barista dan printer
├── *.js                    # Logic tiap halaman dan shared logic
├── styles.css              # CSS tambahan dan aturan print
├── tailwind-config.js      # Konfigurasi warna/utilitas Tailwind
├── supabase-client.js      # Client dan operasi database Supabase
├── setup.sql               # Schema database dan realtime publication
├── api/config.js           # Endpoint konfigurasi deployment
├── supabase/config.toml    # Konfigurasi Supabase lokal
└── .gitignore              # File yang tidak boleh masuk repository
```

## 4. Konvensi Implementasi

- Gunakan JavaScript vanilla dan API browser yang sudah digunakan proyek.
- Pertahankan nama ID HTML karena digunakan oleh JavaScript.
- Pertahankan urutan pemuatan script: library eksternal, konfigurasi, client, shared logic, lalu page logic.
- Gunakan fungsi operasi database di `supabase-client.js` agar akses data tetap terpusat.
- Jangan menaruh service role key di frontend.
- Simpan secret deployment pada environment variable hosting.
- Gunakan komentar `START:` pada blok UI utama bila menambahkan komponen baru.

## 5. Environment Variable Deployment

Endpoint `api/config.js` membaca:

```text
SUPABASE_URL
SUPABASE_KEY
```

Jangan commit file `.env` atau secret key ke repository. Public anon key tetap harus dilindungi dengan konfigurasi database dan policy yang benar.

## 6. Database

Tabel utama:

- `aels_master_products`
- `aels_products`
- `aels_baristas`
- `aels_print_settings`

Schema awal tersedia di `setup.sql`.

## 7. Risiko Teknis yang Perlu Diperhatikan

- CDN membutuhkan koneksi internet saat halaman dimuat.
- Supabase lokal membutuhkan Docker atau Podman.
- Printer jaringan membutuhkan akses dari browser ke alamat printer/service print.
- RLS saat ini dinonaktifkan berdasarkan konfigurasi lama aplikasi; ini perlu ditinjau sebelum penggunaan publik.

## 8. Validasi Minimum

Sebelum commit:

```powershell
node.exe --check dashboard.js
node.exe --check shared.js
git diff --check
```

Sebaiknya semua file JavaScript diperiksa, bukan hanya dua contoh di atas.