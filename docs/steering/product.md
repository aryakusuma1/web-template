# Steering — Product

## 1. Misi Produk

Membangun fondasi aplikasi web yang reusable, aman, mudah dipahami, dan cukup fleksibel untuk berbagai kebutuhan. Keberhasilan diukur dari kemudahan pengembangan fitur berikutnya dan konsistensi kualitas, bukan dari jumlah abstraksi atau fitur bawaan.

## 2. Prioritas Produk

1. Keandalan setup, autentikasi, proteksi akses, dan pola CRUD.
2. Keterbacaan struktur dan pengalaman pengguna yang konsisten.
3. Keamanan dan validasi/otorisasi backend.
4. Pengujian serta dokumentasi yang dapat diikuti.
5. Ekstensibilitas tanpa mengunci template pada satu domain bisnis.

## 3. Batasan Produk

- Jangan menganggap semua aplikasi membutuhkan landing page publik, CMS, e-commerce, atau analitik kompleks.
- Jangan menampilkan data contoh di dashboard seolah data nyata.
- Jangan memasukkan fitur opsional ke MVP sebelum kebutuhan dikonfirmasi.
- Komponen generik tidak boleh bergantung pada istilah atau aturan bisnis satu fitur.

## 4. Pengambilan Keputusan

- Pilih solusi paling sederhana yang memenuhi requirements dan masih memungkinkan perluasan.
- Jika keputusan mengubah scope, alur pengguna, kontrak API, atau arsitektur, perbarui dokumen terkait.
- Catat asumsi yang belum dikonfirmasi; jangan menyajikannya sebagai keputusan final.
- Perubahan visual tidak boleh mengurangi aksesibilitas, keamanan, atau keterbacaan.

## 5. Definisi Selesai dari Sudut Pandang Produk

- Acceptance criteria terpenuhi dan dapat diverifikasi.
- Alur pengguna memiliki feedback yang jelas untuk keadaan berhasil dan gagal.
- Fitur tidak menduplikasi pola yang sudah tersedia tanpa alasan.
- Dokumentasi penggunaan diperbarui jika perilaku atau setup berubah.
