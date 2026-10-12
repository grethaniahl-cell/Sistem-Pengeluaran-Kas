# Pencatatan Kas Keluar

Aplikasi pencatatan jurnal umum berbasis HTML, CSS, JavaScript, dan Supabase (PostgreSQL).

## Struktur folder

```text
AUDIT/
├── README.md
├── backend/
│   └── app.js
├── database/
│   └── schema.sql
└── frontend/
    ├── index.html
    ├── css/
    │   └── style.css
    └── js/
        └── app.js
```

## Persiapan Supabase

1. Buka **SQL Editor** pada project Supabase.
2. Jalankan seluruh isi [`database/schema.sql`](database/schema.sql). Skrip ini membuat tabel, foreign key, constraint debit/kredit, trigger keseimbangan jurnal, penguncian jurnal `posted`, fungsi untuk membuat jurnal dan jurnal pembalik, serta kebijakan akses demo.
3. Gunakan **Project URL** dan **publishable key** dari pengaturan API project Supabase. Jangan gunakan `service_role` key di frontend.
4. Buka `frontend/index.html`, klik **Pengaturan koneksi**, isi Project URL dan publishable key sekali, lalu simpan. Koneksi disimpan pada browser yang digunakan dan dicoba otomatis pada pembukaan berikutnya.

Jika Supabase belum mengenali fungsi jurnal setelah skrip dijalankan, muat ulang halaman aplikasi. Pastikan project Supabase selesai menjalankan SQL tanpa error.

> **Keamanan:** kebijakan `anon` dalam SQL ini ditujukan untuk demo dan memberi akses baca/tulis ke siapa pun yang memiliki URL serta publishable key. Sebelum menggunakan data sungguhan atau memublikasikan aplikasi, ganti kebijakan ini dengan Supabase Auth dan aturan akses yang sesuai.

## Membuka aplikasi

### Membuka frontend langsung

Buka `frontend/index.html` di browser. Frontend menggunakan file lokal dan tidak membutuhkan CDN.

### Menjalankan server statis opsional

Backend sederhana menggunakan modul bawaan Node.js, tanpa `package.json` atau dependensi eksternal. Dari root project:

```powershell
node backend\app.js
```

Buka `http://localhost:4173`. Port dapat diganti melalui environment variable `PORT`.

## Fitur

- Dashboard jurnal dan ringkasan nominal.
- CRUD chart of accounts; akun yang sudah digunakan jurnal tidak dapat dihapus.
- Input jurnal multi-baris dengan kolom debit dan kredit terpisah. Tombol posting hanya aktif jika jurnal valid dan seimbang.
- Validasi keseimbangan juga dilakukan di database.
- Jurnal `posted` tidak dapat diubah atau dihapus; koreksi dilakukan menggunakan jurnal pembalik (storno).
- Laporan ringkasan berdasarkan akun dan klasifikasi laporan.
