# Steering — Tech

## 1. Tumpukan Teknologi

- **Frontend:** Vue.js 3, TypeScript, Vite.
- **Routing:** Vue Router.
- **Styling:** Tailwind CSS.
- **HTTP:** Axios melalui satu API client terpusat.
- **State:** Pinia bila kebutuhan state lintas komponen/fitur muncul.
- **Backend:** Laravel REST API.
- **Database/ORM:** MySQL dan Eloquent.
- **Auth:** Laravel Sanctum sesuai skenario klien.

Versi paket dipilih saat bootstrap dan harus kompatibel serta masih didukung. Jangan mengarang versi atau mengunci versi tanpa memeriksa kebutuhan proyek.

## 2. Batas Tanggung Jawab

- Frontend menangani tampilan, interaksi, validasi ringan untuk UX, dan penyajian error.
- Backend menjadi sumber kebenaran untuk aturan bisnis, validasi, autentikasi, otorisasi, dan perubahan data.
- Frontend tidak mengakses database secara langsung.
- REST API tidak bergantung pada detail UI web sehingga dapat digunakan klien lain.
- Komponen bersama tidak mengandung logika bisnis spesifik.

## 3. Standar API

- Gunakan prefix `/api/v1`.
- Gunakan HTTP method dan status sesuai makna operasi.
- Validasi input di server dan kembalikan error yang dapat ditangani frontend.
- Gunakan pagination server-side untuk daftar data.
- Jangan mengekspos stack trace, kredensial, token, atau detail internal pada respons produksi.
- Perubahan kontrak API harus disertai pembaruan dokumentasi dan test.

## 4. Keamanan

- Jangan commit `.env` atau kredensial; tinjau `.gitignore` dan diff sebelum commit.
- Sediakan `.env.example` dengan placeholder aman.
- Lakukan otorisasi pada operasi privat di backend.
- Konfigurasikan CSRF, CORS, cookie, dan domain sesuai strategi autentikasi.
- Gunakan HTTPS di deployment dan jangan menulis data sensitif ke log.
- Evaluasi dependensi dan hindari memasang paket hanya untuk kebutuhan yang sangat kecil.
- Jangan menyimpan token sensitif di `localStorage` sebagai pilihan default.

## 5. Kualitas dan Pengujian

- Tambahkan test regresi untuk bug yang diperbaiki.
- Uji alur autentikasi, otorisasi, validasi, dan CRUD yang kritis.
- Jalankan test, lint bila tersedia, type-check, dan build yang relevan.
- Jangan melemahkan/menghapus test hanya agar pipeline lulus tanpa memahami penyebabnya.
- Jika pemeriksaan tidak dapat dijalankan, nyatakan secara jujur; jangan mengklaim lulus.

## 6. Alur Kerja Perubahan Kode

1. Baca dokumen dan kode terkait; identifikasi pemanggil serta dampak perubahan.
2. Buat perubahan terkecil yang memenuhi kebutuhan.
3. Periksa diff dan pastikan pekerjaan yang sudah ada tidak tertimpa.
4. Jalankan pemeriksaan yang relevan dan evaluasi hasilnya.
5. Perbarui dokumentasi, task, dan keputusan teknis jika perlu.
6. Ringkas file yang berubah, alasan, test yang dijalankan, dan pekerjaan yang tertunda.

## 7. Konvensi Git

- Gunakan pesan commit yang jelas, misalnya `feat: tambah pengelolaan pengguna`, `fix: perbaiki validasi login`, atau `docs: perbarui panduan pemasangan`.
- Jangan commit build output, cache, file environment rahasia, atau artefak yang tidak diperlukan.
- Hindari force push atau operasi destruktif tanpa kebutuhan jelas dan persetujuan eksplisit.

## 8. Checklist Sebelum Selesai

- [ ] Requirements dan acceptance criteria yang relevan terpenuhi.
- [ ] Autentikasi, otorisasi, dan validasi diperiksa jika perubahan menyentuh akses/data.
- [ ] Tidak ada duplikasi atau abstraksi baru yang tidak perlu.
- [ ] Test/pemeriksaan dijalankan atau keterbatasannya dinyatakan.
- [ ] Tidak ada secret, debug output, atau stack trace terekspos.
- [ ] Dokumentasi dan task diperbarui sesuai kondisi aktual.
