# SDD — Tasks
## Universal Website Starter Template

- **Versi:** 1.0 (Rencana awal)
- **Status tugas:** `Belum dimulai` · `Berjalan` · `Terhambat` · `Selesai`

> Kerjakan bertahap. Jangan membangun semua fitur sekaligus. Perbarui status dan catatan ketika keputusan atau implementasi berubah.

## Tahap 0 — Persiapan dan Keputusan
- [x] T0.1 Konfirmasi cakupan MVP dan keputusan tertunda di `design.md`.
- [x] T0.2 Tetapkan versi Node.js, PHP, Laravel, Composer, dan MySQL yang kompatibel (Node.js >=20, PHP 8.2+/8.3, Composer 2.8+, Laravel 11.x, MySQL 8.4 via Laragon, Vue 3 + TS + Vite).
- [x] T0.3 Tetapkan aturan branch dan commit.
- [x] T0.4 Siapkan repositori Git dan `.gitignore` untuk kedua aplikasi.
- [x] T0.5 Buat README utama dan direktori dokumentasi.

**Kriteria selesai:** struktur dan versi teknologi tercatat; rahasia dan file hasil build tidak dilacak.

## Tahap 1 — Bootstrap Repositori
- [ ] T1.1 Buat proyek Vue 3 + TypeScript + Vite di `frontend/`.
- [ ] T1.2 Pasang dan konfigurasi Vue Router.
- [ ] T1.3 Pasang dan konfigurasi Tailwind CSS sesuai versi yang dipilih.
- [ ] T1.4 Pasang Axios dan buat konfigurasi klien API terpusat.
- [ ] T1.5 Buat proyek Laravel di `backend/`.
- [ ] T1.6 Konfigurasikan koneksi MySQL melalui environment.
- [ ] T1.7 Buat `.env.example` aman untuk kedua aplikasi.
- [ ] T1.8 Pastikan frontend dapat dijalankan dan dibuild.
- [ ] T1.9 Pastikan Laravel dapat dijalankan dan terhubung ke database.

**Kriteria selesai:** aplikasi dasar berjalan secara lokal sesuai panduan.

## Tahap 2 — Fondasi Backend API
- [ ] T2.1 Tetapkan pola endpoint `/api/v1`.
- [ ] T2.2 Tetapkan format respons sukses, pagination, dan kesalahan.
- [ ] T2.3 Konfigurasikan penanganan kesalahan tanpa membocorkan detail internal.
- [ ] T2.4 Konfigurasikan CORS untuk domain pengembangan.
- [ ] T2.5 Tambahkan health-check sederhana jika bermanfaat.
- [ ] T2.6 Dokumentasikan pola API.
- [ ] T2.7 Tambahkan tes untuk kontrak respons dasar.

**Kriteria selesai:** endpoint dasar konsisten dan pengujian terkait lulus.

## Tahap 3 — Autentikasi dan Keamanan
- [ ] T3.1 Pasang dan konfigurasikan Laravel Sanctum.
- [ ] T3.2 Pilih dan dokumentasikan cookie/sesi untuk SPA web.
- [ ] T3.3 Dokumentasikan strategi token untuk klien mobile bila diperlukan.
- [ ] T3.4 Implementasikan login dan logout.
- [ ] T3.5 Implementasikan endpoint pengguna aktif.
- [ ] T3.6 Lindungi endpoint privat dengan middleware.
- [ ] T3.7 Terapkan validasi dan throttling login.
- [ ] T3.8 Konfigurasikan CSRF, CORS, dan stateful domain sesuai lingkungan.
- [ ] T3.9 Implementasikan penanganan sesi kedaluwarsa di frontend.
- [ ] T3.10 Uji login, logout, respons 401, dan akses tanpa izin.

**Kriteria selesai:** alur autentikasi berfungsi dan tes keamanan dasar lulus.

## Tahap 4 — Fondasi Frontend, Tata Letak, dan Halaman Error
- [ ] T4.1 Buat struktur aplikasi/fitur/komponen bersama sesuai rancangan.
- [ ] T4.2 Buat tata letak publik (`PublicLayout.vue`) dengan top navbar, content container, dan footer.
- [ ] T4.3 Buat halaman Home/Landing page publik (`HomePage.vue`) dengan hero, fitur, tech showcase, dan CTA.
- [ ] T4.4 Buat tata letak admin (`AdminLayout.vue`) dengan sidebar navigasi kiri (collapsible & mobile drawer).
- [ ] T4.5 Buat tata letak auth (`AuthLayout.vue`) dan halaman login (`LoginPage.vue`).
- [ ] T4.6 Buat halaman penanganan error: `NotFoundPage.vue` (404), `ForbiddenPage.vue` (403), `ServerErrorPage.vue` (500).
- [ ] T4.7 Buat guard rute Vue Router berdasarkan status autentikasi dan penanganan rute catch-all 404.
- [ ] T4.8 Buat katalog komponen bersama eksplisit:
  - Buttons: `BaseButton.vue`, `IconButton.vue`
  - Forms: `FormField.vue`, `BaseInput.vue`, `BaseTextarea.vue`, `BaseSelect.vue`, `BaseCheckbox.vue`, `BaseSwitch.vue`
  - Feedback: `BaseAlert.vue`, `BaseToast.vue`, `LoadingSpinner.vue`, `EmptyState.vue`, `ErrorState.vue`
  - Data: `DataTable.vue`, `Pagination.vue`, `BaseBadge.vue`, `BaseCard.vue`
  - Overlays: `BaseModal.vue`, `ConfirmDialog.vue`, `BaseDropdown.vue`
  - Navigation: `Breadcrumbs.vue`
- [ ] T4.9 Uji responsivitas desktop dan mobile.

**Kriteria selesai:** tata letak publik dan admin konsisten, halaman error berfungsi, dan komponen bersama siap pakai.

## Tahap 5 — Pengguna dan Otorisasi (Modul CRUD 1)
- [ ] T5.1 Rancang migration dan model `User`.
- [ ] T5.2 Tentukan pendekatan peran (`admin`, `user`) dan status aktif/nonaktif.
- [ ] T5.3 Implementasikan `UserPolicy` dan middleware otorisasi.
- [ ] T5.4 Buat Form Request (`StoreUserRequest`, `UpdateUserRequest`).
- [ ] T5.5 Buat API Resource `UserResource`.
- [ ] T5.6 Implementasikan `UserController` (index, store, show, update, destroy).
- [ ] T5.7 Terapkan pencarian, filter role/status, dan pagination server.
- [ ] T5.8 Buat frontend `UserListPage.vue`, `UserDetailPage.vue`, `UserFormPage.vue`.
- [ ] T5.9 Hubungkan konfirmasi hapus dengan `ConfirmDialog`.
- [ ] T5.10 Uji backend feature test (`UserCrudTest`) dan alur frontend.

**Kriteria selesai:** pengelolaan pengguna berfungsi penuh dengan validasi dan otorisasi teruji.

## Tahap 6 — Modul Post dan Pola CRUD Universal (Modul CRUD 2)
- [ ] T6.1 Buat dashboard dasar dengan statistik nyata dari User dan Post.
- [ ] T6.2 Rancang migration dan model `Post` (title, slug, content, status draft/published, author_id).
- [ ] T6.3 Buat Form Request (`StorePostRequest`, `UpdatePostRequest`) dengan validasi slug dan status.
- [ ] T6.4 Buat `PostResource` dengan data author tersemat.
- [ ] T6.5 Buat `PostPolicy` (author dan admin yang berhak mengedit/menghapus).
- [ ] T6.6 Implementasikan `PostController` (index, store, show, update, destroy) dengan filter status & pencarian.
- [ ] T6.7 Buat frontend `PostListPage.vue`, `PostDetailPage.vue`, `PostFormPage.vue`.
- [ ] T6.8 Terapkan composable `usePosts.ts` dan service `postApi.ts`.
- [ ] T6.9 Buat pengujian otomatis backend (`PostCrudTest`).
- [ ] T6.10 Dokumentasikan panduan replikasi CRUD baru berdasarkan modul User dan Post.

**Kriteria selesai:** dua modul CRUD lengkap berjalan sebagai acuan baku yang konsisten dan dapat direplikasi dengan mudah.

## Tahap 7 — Kualitas, Pengujian, dan Dokumentasi
- [ ] T7.1 Tambahkan pengujian frontend untuk alur kritis.
- [ ] T7.2 Pastikan seluruh feature test backend lulus.
- [ ] T7.3 Pastikan pemeriksaan tipe (`vue-tsc --noEmit`) dan build frontend (`vite build`) lulus.
- [ ] T7.4 Tinjau aksesibilitas formulir, keyboard focus, dan error messaging.
- [ ] T7.5 Tinjau rahasia dan konfigurasi environment (`.env.example`).
- [ ] T7.6 Tulis panduan instalasi lokal dan migrasi database.
- [ ] T7.7 Tulis panduan deployment, CORS, dan autentikasi.
- [ ] T7.8 Perbarui README dengan perintah yang sudah diverifikasi.

**Kriteria selesai:** dokumentasi dapat diikuti dan seluruh pengujian kualitas lulus.

## Tahap 8 — Fitur Lanjutan (Opsional Pasca-MVP)
- [ ] O8.1 Tema gelap (Dark mode toggle & styling).
- [ ] O8.2 Log aktivitas audit (Audit trails).
- [ ] O8.3 Notifikasi real-time (WebSockets).
- [ ] O8.4 Ekspor file (CSV / Excel / PDF).
- [ ] O8.5 Izin granular dinamis (Role & Permission matrix).
- [ ] O8.6 Fitur domain khusus (E-commerce / Multi-tenant).

## Aturan Pengerjaan

Sebelum mengerjakan tugas:
1. Baca kebutuhan terkait di `requirements.md`.
2. Periksa keputusan dan struktur di `design.md`.
3. Cari implementasi yang sudah ada sebelum menambah kode.
4. Implementasikan satu irisan kecil yang dapat diuji.
5. Jalankan tes/pemeriksaan relevan.
6. Perbarui dokumentasi dan status tugas.
7. Catat keputusan baru di `steering.md` bila memengaruhi pola lintas proyek.
