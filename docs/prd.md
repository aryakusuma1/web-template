# Product Requirements Document (PRD)
## Universal Website Starter Template

- **Versi:** 1.0 (Draft)
- **Bahasa dokumentasi:** Bahasa Indonesia
- **Frontend:** Vue 3, TypeScript, Vite, Vue Router, Tailwind CSS, Axios
- **Backend:** Laravel REST API
- **Database:** MySQL dengan Eloquent ORM
- **Pola repositori:** satu repositori berisi `frontend/` dan `backend/`

## 1. Ringkasan Produk

Universal Website Starter Template adalah fondasi awal yang dapat digunakan ulang untuk membangun berbagai aplikasi web. Template menyediakan struktur proyek, autentikasi, tata letak admin, pengelolaan pengguna, komponen UI bersama, pola CRUD, standar REST API, pengujian dasar, dan dokumentasi.

Frontend dan backend dipisahkan sebagai aplikasi berbeda dalam satu repositori. Frontend berkomunikasi dengan backend melalui REST API sehingga backend dapat digunakan kembali oleh klien lain, termasuk aplikasi mobile Flutter.

## 2. Masalah yang Ingin Diselesaikan

1. Proyek baru sering mengulang implementasi autentikasi, tata letak, formulir, tabel, validasi, dan CRUD.
2. Pengulangan kode menyebabkan perilaku dan tampilan tidak konsisten.
3. Penambahan fitur tanpa pedoman arsitektur membuat folder dan kode berantakan.
4. Struktur yang terlalu khusus untuk satu jenis aplikasi sulit digunakan ulang.

## 3. Tujuan

- Mempercepat inisiasi proyek baru.
- Membuat struktur folder dan penamaan mudah dipahami.
- Mendorong penggunaan ulang tanpa abstraksi berlebihan.
- Memisahkan UI, logika bisnis, dan akses data.
- Menyediakan REST API yang dapat digunakan web dan klien lain.
- Menjaga keamanan, kemudahan pengujian, dan dokumentasi.

### Indikator keberhasilan

- Pengembang dapat menjalankan frontend dan backend dengan mengikuti panduan.
- Autentikasi, pengelolaan pengguna, dan kontrol akses berfungsi.
- Modul baru dapat ditambahkan mengikuti pola yang ada tanpa menyalin kode secara tidak perlu.
- Endpoint API memiliki validasi, respons, penanganan kesalahan, dan pengujian yang konsisten.
- Tidak ada kredensial rahasia di repositori.

## 4. Pengguna Sasaran

- Pengembang individu yang memulai aplikasi web.
- Tim kecil yang memerlukan fondasi proyek konsisten.
- Pengembang frontend dan backend yang membutuhkan batas tanggung jawab jelas.
- Pengembang aplikasi mobile yang menggunakan backend API yang sama.

## 5. Prinsip Produk

1. **Gunakan kembali sebelum membuat baru.** Cari komponen, layanan, utilitas, dan pola yang sudah ada.
2. **Sederhana terlebih dahulu.** Abstraksi dibuat hanya jika memberi manfaat nyata.
3. **Satu tanggung jawab.** Setiap modul dan berkas memiliki tujuan yang jelas.
4. **Berbasis fitur.** Kode khusus fitur dikelompokkan berdasarkan domain.
5. **Hormati konvensi framework.** Nama bawaan Laravel, Vue, Vite, Composer, dan tooling tidak diterjemahkan.
6. **Bahasa Indonesia untuk dokumentasi dan domain.** Istilah teknis baku dan nama API boleh tetap berbahasa Inggris.
7. **Aman secara bawaan.** Validasi server, otorisasi, perlindungan rahasia, dan pengujian dasar wajib diperhatikan.
8. **Fitur opsional tidak dipaksakan ke inti.**

## 6. Cakupan MVP

### Termasuk

- Monorepo dengan `frontend/` dan `backend/`.
- Vue 3 + TypeScript + Vite, Vue Router, Tailwind CSS, dan Axios.
- Laravel REST API dengan versi rute `/api/v1`.
- MySQL dan Eloquent ORM.
- `.env.example` untuk kedua aplikasi.
- Tata letak publik (`PublicLayout`) dengan top navigation bar, container konten, dan footer.
- Halaman Home / Landing Page publik (Hero, showcase fitur, teknologi, dan CTA login/dashboard).
- Tata letak admin (`AdminLayout`) dengan sidebar navigasi kiri responsif (collapsible / mobile drawer) dan header profil.
- Tata letak autentikasi terisolasi (`AuthLayout`) untuk halaman login.
- Halaman penanganan error informatif: 404 (Not Found), 403 (Forbidden), dan 500 (Server Error).
- Login, logout, dan informasi pengguna aktif dengan Laravel Sanctum.
- Perlindungan rute frontend (Navigation Guards) dan endpoint backend (Middleware & Policies).
- Dua modul CRUD lengkap sebagai acuan arsitektur:
  1. **Pengelolaan Pengguna (`users`):** Pencarian, filter status/role, pagination server, tambah, ubah, nonaktifkan/hapus.
  2. **Pengelolaan Konten/Post (`posts`):** Representasi entitas bisnis dengan relasi ke user (`author_id`), status workflow (`draft`/`published`), generator slug, pencarian, dan pagination.
- Komponen UI bersama eksplisit: BaseButton, IconButton, FormField, BaseInput, BaseTextarea, BaseSelect, BaseCheckbox, BaseSwitch, BaseAlert, BaseToast, LoadingSpinner, EmptyState, ErrorState, DataTable, Pagination, BaseBadge, BaseCard, BaseModal, ConfirmDialog, BaseDropdown, Breadcrumbs.
- Penanganan 5 kondisi UI: loading, empty, error, success (toast), dan validasi per-field (422).
- Pola respons API, validasi Form Request, API Resource, dan dokumentasi endpoint.
- Pengujian otomatis dasar dan panduan pengembangan.

### Tidak termasuk dalam MVP (Dilewati / Ditunda)

- Tema gelap (Dark mode) — dilewati agar fokus pada estetika dan ketajaman Light mode.
- E-commerce, payment gateway, multi-tenant kompleks, dan approval workflow rumit.
- Chat, WebSocket, notifikasi real-time.
- Ekspor PDF/Excel lanjutan.
- Integrasi layanan pihak ketiga berbayar/khusus.

## 7. Kebutuhan Fungsional

| ID | Kebutuhan | Prioritas |
|---|---|---|
| F-01 | Pengguna dapat login dan logout dengan mekanisme autentikasi yang dikonfigurasi secara aman. | Wajib |
| F-02 | Sistem menampilkan informasi pengguna aktif. | Wajib |
| F-03 | Halaman dan endpoint privat terlindungi dari akses tanpa autentikasi. | Wajib |
| F-04 | Administrator dapat mengelola pengguna (CRUD users: pencarian, filter, pagination, validasi, otorisasi). | Wajib |
| F-05 | Pengguna dapat mengelola konten (CRUD posts: relasi author, status draft/published, slug, pagination). | Wajib |
| F-06 | Sistem menyediakan halaman publik Home/Landing page dengan tata letak top navigation (`PublicLayout`). | Wajib |
| F-07 | Sistem menyediakan tata letak admin responsif (`AdminLayout`) dengan sidebar kiri dan mobile drawer. | Wajib |
| F-08 | Sistem menyediakan halaman penanganan error khusus: 404 (Not Found), 403 (Forbidden), dan 500 (Server Error). | Wajib |
| F-09 | CRUD dan antarmuka memiliki penanganan keadaan: loading, empty, sukses, validasi, dan gagal. | Wajib |
| F-10 | Frontend menggunakan konfigurasi klien API Axios terpusat dengan interceptor standar. | Wajib |
| F-11 | Backend memvalidasi input via Form Request dan mengembalikan respons terstruktur via API Resource. | Wajib |
| F-12 | Modul baru dapat ditambahkan dengan mengikuti pola terdokumentasi dari dua modul acuan. | Wajib |
| F-13 | Alur kritis memiliki pengujian otomatis (backend feature tests dan frontend type/build check). | Wajib |

## 8. Kebutuhan Nonfungsional

- **Pemeliharaan:** tanggung jawab tiap modul jelas; jangan membuat folder kosong tanpa alasan.
- **Keterbacaan:** fungsi, komponen, dan kelas memiliki tujuan yang jelas.
- **Reuse:** komponen bersama tidak memuat logika khusus satu fitur.
- **Keamanan:** validasi server, otorisasi, CSRF sesuai strategi autentikasi, throttling, dan pengelolaan rahasia.
- **Kinerja:** pagination server untuk daftar besar dan pemuatan data seperlunya.
- **Aksesibilitas:** label input, navigasi keyboard, fokus terlihat, dan pesan kesalahan yang jelas.
- **Responsif:** mendukung desktop, tablet, dan ponsel.
- **Pengujian:** perilaku penting dapat diuji otomatis.
- **Portabilitas:** konfigurasi lokal, staging, dan produksi dipisahkan.
- **Dokumentasi:** pemasangan dan penambahan fitur dapat diikuti tanpa menebak.

## 9. Arsitektur Tingkat Tinggi

```text
Pengguna
   ↓
Frontend Vue 3 + TypeScript
   ↓ HTTP/JSON
Laravel REST API (/api/v1)
   ↓ Eloquent ORM
MySQL
```

Frontend dan backend dapat dikembangkan serta diterapkan secara terpisah. Frontend tidak mengakses database secara langsung.

## 10. Strategi Autentikasi

Gunakan Laravel Sanctum sesuai jenis klien:

- Untuk SPA web pihak pertama, prioritaskan cookie/sesi dengan konfigurasi domain, CORS, dan CSRF yang benar.
- Untuk aplikasi mobile atau klien token, gunakan token Sanctum bila diperlukan.
- Jangan menjadikan `localStorage` sebagai tempat default untuk token sensitif tanpa mengevaluasi risiko XSS.
- Otorisasi wajib dilakukan di backend.

## 11. Risiko dan Mitigasi

| Risiko | Mitigasi |
|---|---|
| Template terlalu rumit | Bangun MVP terlebih dahulu dan tunda modul opsional. |
| Duplikasi kode | Cari implementasi yang sudah ada sebelum membuat yang baru. |
| Abstraksi berlebihan | Tidak wajib membuat repository/service/interface untuk setiap CRUD sederhana. |
| Nama Indonesia bertentangan dengan konvensi framework | Pertahankan nama wajib framework; gunakan Bahasa Indonesia untuk domain dan dokumentasi. |
| Konfigurasi autentikasi tidak cocok untuk semua klien | Dokumentasikan konfigurasi SPA dan token secara terpisah. |
| Perubahan merusak fitur lama | Tambahkan pengujian regresi dan periksa dampak komponen bersama. |

## 12. Kriteria Selesai MVP

- Frontend dan backend dapat dipasang dan dijalankan mengikuti panduan.
- Login/logout, pengguna aktif, perlindungan rute, dan otorisasi bekerja.
- Pengelolaan pengguna dan pola CRUD dasar tersedia.
- Validasi dan kesalahan ditampilkan secara konsisten.
- Pengujian penting lulus.
- Tidak ada rahasia di repositori.
- Struktur dan pola penambahan fitur terdokumentasi.
