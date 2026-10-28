# SDD — Requirements
## Universal Website Starter Template

- **Versi:** 1.0 (Draft)
- **Bahasa:** Bahasa Indonesia

## 1. Tujuan

Dokumen ini menjabarkan kebutuhan perangkat lunak yang menjadi acuan desain, implementasi, dan pengujian.

## 2. Ruang Lingkup

Fondasi aplikasi web full-stack dengan frontend Vue 3 + TypeScript dan backend Laravel REST API menggunakan MySQL. Cakupan MVP meliputi:

- **Tata letak:** `PublicLayout` (halaman publik dengan top navigation), `AdminLayout` (sidebar kiri responsif), dan `AuthLayout` (formulir login terisolasi).
- **Halaman publik:** Landing page/Home page sebagai pintu masuk aplikasi dan pengenalan template.
- **Autentikasi:** login, logout, dan pengguna aktif via Laravel Sanctum.
- **Dua modul CRUD acuan:** pengelolaan pengguna (`users`) dan pengelolaan konten/post (`posts`).
- **Komponen UI bersama:** katalog lengkap komponen generik (tombol, formulir, feedback, tabel, overlay, navigasi).
- **Halaman penanganan error:** 404, 403, dan 500 dengan pesan informatif dan opsi pemulihan.

Modul domain khusus (e-commerce, CMS, multi-tenant, notifikasi real-time) dan fitur opsional (dark mode, ekspor) bukan bagian dari MVP dan tidak boleh dipaksakan ke inti template.

## 3. Aktor dan Hak Akses

- **Pengunjung:** hanya dapat melihat halaman publik yang memang tersedia, termasuk halaman login; tidak dapat mengakses endpoint privat.
- **Pengguna terautentikasi:** dapat melihat data akunnya dan melakukan tindakan yang diizinkan.
- **Administrator:** dapat membuka dashboard dan mengelola pengguna sesuai kebijakan backend.

Peran dan izin tidak boleh hanya diterapkan dengan menyembunyikan elemen UI. Semua endpoint privat harus melakukan pemeriksaan di backend.

## 4. Kebutuhan Fungsional

### AUT — Autentikasi
- **AUT-01:** Pengguna dapat login dengan kredensial valid.
- **AUT-02:** Kredensial tidak valid menghasilkan pesan umum yang tidak membocorkan apakah email tertentu terdaftar.
- **AUT-03:** Pengguna dapat logout.
- **AUT-04:** Frontend dapat mengambil data pengguna aktif.
- **AUT-05:** Permintaan tanpa autentikasi valid ditolak untuk endpoint privat.
- **AUT-06:** Sesi kedaluwarsa atau respons 401 ditangani secara konsisten.
- **AUT-07:** Strategi cookie/sesi untuk SPA dan token untuk klien mobile didokumentasikan terpisah.

### PGL — Pengelolaan Pengguna (Modul CRUD 1)
- **PGL-01:** Administrator dapat melihat daftar pengguna.
- **PGL-02:** Daftar mendukung pencarian, filter relevan (role, status), dan pagination server.
- **PGL-03:** Administrator dapat membuat dan memperbarui data pengguna.
- **PGL-04:** Penghapusan atau penonaktifan mengikuti aturan integritas data.
- **PGL-05:** Validasi server menampilkan kesalahan per bidang (422).
- **PGL-06:** Pengguna tidak dapat meningkatkan hak aksesnya melalui manipulasi permintaan.

### PST — Pengelolaan Post/Konten (Modul CRUD 2)
- **PST-01:** Pengguna dapat melihat daftar post dengan pagination server, pencarian judul, dan filter status.
- **PST-02:** Pengguna dapat membuat post baru dengan status (`draft` / `published`), konten, dan slug unik.
- **PST-03:** Post memiliki relasi foreign key ke pengguna (`author_id`).
- **PST-04:** Otorisasi diterapkan melalui Policy (author dan admin yang berhak mengedit/menghapus).
- **PST-05:** Form post menangani validasi error 422 untuk judul, slug, dan status.

### LAY — Tata Letak dan Halaman Publik
- **LAY-01:** `PublicLayout` menyediakan sticky top navigation bar, container responsif, dan footer.
- **LAY-02:** Halaman Home/Landing page menyajikan hero banner, pengenalan fitur starter, tech stack showcase, dan navigasi CTA.
- **LAY-03:** `AdminLayout` menyediakan sidebar navigasi kiri (collapsible di desktop, drawer overlay di mobile), header profil pengguna, breadcrumbs, dan area konten responsif.
- **LAY-04:** `AuthLayout` menyediakan kartu formulir login yang terisolasi dan terpusat.

### ERR — Penanganan Error dan UI Fallback
- **ERR-01:** Halaman 404 (Not Found) ditampilkan saat rute frontend tidak ditemukan atau ID data tidak ada di API, dilengkapi tombol kembali ke Beranda dan Dashboard.
- **ERR-02:** Halaman 403 (Forbidden) ditampilkan saat pengguna tidak memiliki hak akses/izin ke halaman tertentu.
- **ERR-03:** Halaman 500 (Server Error) menangani kegagalan internal server tanpa membocorkan trace sensitif, dilengkapi tombol muat ulang halaman.

### DAS — Dashboard
- **DAS-01:** Dashboard menyediakan tata letak dan area ringkasan.
- **DAS-02:** Angka ringkasan harus berasal dari data nyata; placeholder diberi label jelas dan tidak disajikan sebagai data produksi.

### CRUD — Pola CRUD
- **CRUD-01:** Dua modul acuan (`users` dan `posts`) menjadi standar pola list, detail, create, edit, dan delete.
- **CRUD-02:** Daftar mendukung loading, empty, error, pagination, dan pencarian/filter.
- **CRUD-03:** Dialog konfirmasi (`ConfirmDialog`) digunakan untuk tindakan destruktif.
- **CRUD-04:** Validasi server adalah sumber kebenaran.
- **CRUD-05:** Komponen dan layanan yang sesuai digunakan kembali; halaman utuh tidak disalin begitu saja untuk setiap fitur.

### API — REST API
- **API-01:** Endpoint bisnis berada di bawah `/api/v1`.
- **API-02:** Metode HTTP dan status respons sesuai kegunaannya.
- **API-03:** Validasi menggunakan Form Request untuk setiap operasi mutasi data.
- **API-04:** Keluaran API menggunakan API Resource terstruktur.
- **API-05:** Kesalahan validasi (422), autentikasi (401), otorisasi (403), tidak ditemukan (404), dan server (500) ditangani konsisten.
- **API-06:** Daftar besar menggunakan pagination server.
- **API-07:** Endpoint privat dilindungi middleware dan kebijakan otorisasi.
- **API-08:** API didokumentasikan dan diuji.

### KOMP — Komponen Bersama
- **KOMP-01:** Sediakan katalog komponen bersama eksplisit:
  - **Buttons:** `BaseButton.vue` (variants: primary/secondary/danger/outline/ghost, sizes: sm/md/lg, loading state, slot icons) dan `IconButton.vue`.
  - **Forms:** `FormField.vue` (label, required asterisk, hint, error message), `BaseInput.vue`, `BaseTextarea.vue`, `BaseSelect.vue`, `BaseCheckbox.vue`, `BaseSwitch.vue`.
  - **Feedback:** `BaseAlert.vue`, `BaseToast.vue` (floating flash toast), `LoadingSpinner.vue`, `EmptyState.vue`, `ErrorState.vue` (dengan tombol coba lagi).
  - **Data Display:** `DataTable.vue` (tipe generik, slot per-kolom, empty/loading handler), `Pagination.vue` (page number, per-page selector), `BaseBadge.vue`, `BaseCard.vue`.
  - **Overlays:** `BaseModal.vue` (backdrop, escape key, focus trapping), `ConfirmDialog.vue` (konfirmasi aksi destruktif), `BaseDropdown.vue`.
  - **Navigation:** `Breadcrumbs.vue`.
- **KOMP-02:** Komponen generik tidak mengandung aturan bisnis khusus fitur.
- **KOMP-03:** Komponen memperhatikan keyboard, label, fokus, disabled, dan error state.

### KONF — Konfigurasi dan Pemeliharaan
- **KONF-01:** Rahasia disimpan di environment, bukan kode.
- **KONF-02:** `.env.example` mencantumkan variabel yang diperlukan tanpa rahasia.
- **KONF-03:** Tersedia panduan pemasangan lokal dan konfigurasi produksi.
- **KONF-04:** Aturan penamaan, struktur, reuse, dan pengujian terdokumentasi.
- **KONF-05:** Abstraksi tidak dibuat hanya demi mengikuti pola yang tidak diperlukan.

## 5. Kebutuhan Nonfungsional

- **NFR-01 Pemeliharaan:** tanggung jawab setiap modul jelas.
- **NFR-02 Keamanan:** validasi, autentikasi, otorisasi, CSRF sesuai mode, dan pengelolaan rahasia.
- **NFR-03 Kinerja:** pagination server dan pemuatan data seperlunya.
- **NFR-04 Aksesibilitas:** formulir berlabel, fokus terlihat, navigasi keyboard.
- **NFR-05 Responsif:** mendukung layar kecil dan besar.
- **NFR-06 Pengujian:** alur kritis memiliki pengujian otomatis.
- **NFR-07 Portabilitas:** konfigurasi lingkungan terpisah.
- **NFR-08 Konsistensi:** format API dan keadaan UI mengikuti pola bersama.
- **NFR-09 Dokumentasi:** keputusan arsitektur dan cara menambah fitur tercatat.

## 6. Aturan Validasi dan Kesalahan

- Validasi keamanan dan integritas selalu dilakukan di backend.
- Validasi frontend hanya membantu pengalaman pengguna, bukan menggantikan validasi server.
- Kesalahan validasi menggunakan HTTP `422`.
- Permintaan tidak terautentikasi menggunakan `401`; tidak memiliki izin menggunakan `403`; sumber daya tidak ditemukan menggunakan `404`.
- Kesalahan server tidak menampilkan stack trace atau rahasia kepada klien.
- Respons tidak boleh membocorkan data sensitif.

## 7. Asumsi dan Batasan

- MySQL adalah database awal.
- Frontend dan backend berada dalam satu repositori, tetapi dapat diterapkan terpisah.
- Template tidak mengasumsikan semua proyek membutuhkan CMS, transaksi, workflow, atau halaman publik.
- Konvensi framework tetap diikuti.
- Konfigurasi autentikasi akhir bergantung pada domain deployment dan jenis klien.

## 8. Kriteria Penerimaan

- Instalasi dapat diikuti dari dokumentasi.
- Alur autentikasi dan perlindungan akses lulus pengujian.
- Pengelolaan pengguna memiliki validasi dan otorisasi.
- Daftar menggunakan pagination server.
- Respons API dan kesalahan konsisten.
- Komponen bersama tidak mengandung logika domain yang tidak relevan.
- Tidak ada kredensial rahasia di repositori.
- Perubahan utama memiliki pengujian yang sesuai.
