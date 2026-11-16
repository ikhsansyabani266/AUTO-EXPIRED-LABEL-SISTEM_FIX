# UI/UX Guidelines

## 1. Prinsip Desain

AELS menggunakan gaya antarmuka operasional yang sederhana, cepat dipindai, dan cocok untuk penggunaan coffee shop.

Prinsip utama:

- **Clarity:** status produk dan tindakan utama mudah ditemukan.
- **Speed:** input dan cetak label memiliki langkah minimum.
- **Consistency:** sidebar, top app bar, button, modal, dan toast konsisten antar halaman.
- **Feedback:** setiap operasi penting memberikan status berhasil/gagal.
- **Responsive:** layout mendukung desktop dan mobile.
- **Print-first:** area cetak tidak boleh terganggu oleh elemen navigasi.

## 2. Struktur Layout

Setiap halaman utama menggunakan pola:

```text
Body
├── Print area tersembunyi
├── Sidebar navigation
│   ├── Brand header
│   ├── Navigation links
│   └── Printer status footer
├── Mobile navigation overlay
└── Main content
    ├── Top app bar
    └── Page-specific content
```

## 3. Komponen Utama

### Sidebar Navigation

- Menampilkan identitas AELS.
- Menyediakan link ke Dashboard, Cetak Label, Data Produk, Input Produk, dan Pengaturan.
- Menampilkan status printer.
- Memiliki variasi desktop dan mobile.

### Top App Bar

- Menampilkan judul halaman.
- Menyediakan tindakan kontekstual jika diperlukan.
- Tetap terlihat ketika konten halaman panjang.

### Form

- Label field harus jelas.
- Field wajib divalidasi sebelum submit.
- Nilai default boleh digunakan jika berasal dari master product.
- Error harus ditampilkan dekat dengan konteks tindakan.

### Toast dan Modal

- Gunakan toast untuk feedback singkat.
- Gunakan modal untuk konfirmasi, pengelolaan barista, dan tindakan destruktif.
- Tombol cancel harus selalu tersedia pada tindakan yang dapat dibatalkan.

### Status Produk

Gunakan makna status yang konsisten:

- Hijau: aman/aktif.
- Kuning/oranye: mendekati kedaluwarsa.
- Merah: kedaluwarsa atau membutuhkan tindakan.

Warna harus tetap didukung oleh teks atau ikon agar tidak hanya bergantung pada warna.

## 4. Aksesibilitas

- Semua gambar wajib memiliki `alt` yang bermakna.
- Tombol menggunakan elemen `<button>`, bukan elemen dekoratif.
- Input memiliki label yang jelas.
- Fokus keyboard tidak boleh dihilangkan tanpa alternatif.
- Kontras teks dan background harus tetap terbaca.
- Ikon yang hanya dekoratif tidak boleh menjadi satu-satunya informasi.
- Modal harus dapat ditutup dengan kontrol yang jelas.

## 5. Print UX

- Navigasi dan elemen non-print menggunakan class `no-print`.
- Print area harus memiliki format label yang konsisten.
- Jangan menambahkan elemen interaktif ke dalam hasil cetak.
- Perubahan ukuran label harus diuji pada printer thermal sebenarnya.
- Pastikan tanggal kedaluwarsa terbaca pada hasil cetak.

## 6. Responsif

### Desktop

- Sidebar tampil permanen.
- Main content menggunakan area fleksibel.
- Tabel dan panel dapat memanfaatkan ruang horizontal.

### Mobile

- Sidebar berubah menjadi menu overlay.
- Tombol menu harus mudah dijangkau.
- Form menggunakan satu kolom jika ruang sempit.
- Tabel perlu tetap dapat dibaca melalui scroll horizontal atau layout alternatif yang sudah tersedia.

## 7. Aturan Perubahan UI

- Jangan mengubah class Tailwind atau CSS global tanpa kebutuhan yang jelas.
- Pertahankan ID elemen yang digunakan JavaScript.
- Tambahkan penanda komentar pada blok besar:

```html
<!-- START: Nama Komponen -->
<!-- END: Nama Komponen -->
```

- Uji desktop dan mobile setelah perubahan.
- Uji alur input, simpan, cetak, edit, dan hapus.

## 8. Checklist UX Sebelum Merge

- [ ] Navigasi semua halaman masih berfungsi.
- [ ] Status aktif sidebar sesuai halaman.
- [ ] Form dapat diisi dengan keyboard.
- [ ] Feedback operasi tampil.
- [ ] Data kosong memiliki tampilan yang jelas.
- [ ] Konfirmasi tersedia untuk operasi destruktif.
- [ ] Print preview tetap benar.
- [ ] Tidak ada perubahan visual yang tidak direncanakan.