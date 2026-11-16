# Developer Instructions

## 1. Tujuan Dokumen

Dokumen ini menjadi panduan kerja untuk pengembangan, refactoring, pengujian, dan deployment AELS.

## 2. Sebelum Mengubah Kode

1. Baca file yang akan diubah dan file dependensinya.
2. Cari semua penggunaan ID, function, nama tabel, dan asset terkait.
3. Pastikan perubahan tidak mengubah workflow yang sudah berjalan.
4. Periksa status Git sebelum mulai.
5. Tentukan validasi yang akan dijalankan setelah perubahan.

## 3. Aturan Perubahan Kode

- Pertahankan struktur multi-page yang sedang digunakan.
- Jangan mengganti framework atau menambah library tanpa kebutuhan dan persetujuan teknis.
- Jangan mengubah layout atau styling jika tugas hanya berkaitan dengan dokumentasi/refactoring.
- Jangan mengganti ID HTML tanpa memperbarui JavaScript yang menggunakannya.
- Jangan mengganti nama tabel/database field tanpa migration dan pembaruan mapping.
- Gunakan fungsi data access di `supabase-client.js`.
- Hindari duplikasi implementasi yang sudah tersedia di `shared.js`.
- Tambahkan komentar tingkat blok, bukan komentar di setiap baris.
- Gunakan tag komentar berikut untuk komponen utama:

```html
<!-- START: Component Name -->
<!-- END: Component Name -->
```

```javascript
// START: Feature Name
// END: Feature Name
```

## 4. Aturan Keamanan

- Jangan commit `.env`, password, service role key, atau token private.
- Jangan menaruh service role key di browser.
- Gunakan anon key hanya dengan policy database yang aman.
- Tinjau kembali RLS sebelum deployment publik.
- Jangan menampilkan detail credential pada log atau dokumentasi.
- Validasi input sebelum operasi insert/update.

## 5. Workflow Development

### Memulai Pekerjaan

```powershell
git status --short
Get-ChildItem -Force
```

### Menjalankan Pemeriksaan JavaScript

```powershell
Get-ChildItem -File -Filter '*.js' | ForEach-Object {
    node.exe --check $_.FullName
}
```

### Memeriksa Referensi dan Diff

```powershell
git diff --check
git diff --stat
git status --short
```

### Menjalankan Aplikasi Statis

Jika Python tersedia:

```powershell
python -m http.server 8000
```

Buka:

```text
http://localhost:8000/index.html
```

Jangan hanya mengandalkan `file://` jika fitur fetch atau API endpoint sedang diuji.

## 6. Pengujian Manual Minimum

- Buka dashboard.
- Navigasikan semua menu sidebar.
- Tambahkan atau pilih master produk.
- Buat label dengan tanggal buka dan masa simpan.
- Pastikan tanggal kedaluwarsa benar.
- Simpan dan cetak label.
- Buka riwayat data produk.
- Edit dan hapus data sesuai kebutuhan.
- Kelola barista.
- Periksa pengaturan printer.
- Uji tampilan mobile.
- Uji print preview.

## 7. Supabase Local Development

Supabase lokal memerlukan Docker Desktop atau Podman.

File terkait:

- `supabase/config.toml`
- `setup.sql`
- `supabase/.gitignore`

Jika Docker/Podman belum tersedia, lakukan validasi syntax dan referensi file tanpa mengklaim database lokal berhasil dijalankan.

## 8. Deployment

1. Push source code ke repository Git.
2. Hubungkan repository ke Vercel atau static hosting.
3. Set `SUPABASE_URL` dan `SUPABASE_KEY` sebagai environment variables.
4. Jalankan `setup.sql` pada project Supabase tujuan.
5. Pastikan domain hosting diizinkan oleh konfigurasi Supabase.
6. Uji API config, sinkronisasi database, dan print workflow.
7. Jangan memasukkan binary lokal atau folder temporary ke commit.

## 9. Pull Request Checklist

- [ ] Scope perubahan jelas.
- [ ] Tidak ada secret yang ikut commit.
- [ ] Tidak ada file temporary atau binary tool lokal.
- [ ] Syntax JavaScript lolos.
- [ ] Referensi asset lokal valid.
- [ ] `git diff --check` lolos.
- [ ] Layout dan workflow tidak berubah tanpa requirement.
- [ ] Dokumentasi diperbarui jika behavior berubah.
- [ ] Pengujian manual dijelaskan.

## 10. Commit Convention

Gunakan pesan commit yang singkat dan deskriptif, misalnya:

```text
feat: add product expiry workflow
fix: correct label expiry calculation
refactor: organize shared UI helpers
docs: add project development guide
chore: update gitignore
```

## 11. Prinsip Akhir

Prioritaskan perubahan kecil, dapat ditinjau, mudah dibatalkan, dan tervalidasi. Jangan melakukan refactoring besar jika tidak diperlukan oleh requirement.