# SDD — Design
## Universal Website Starter Template

- **Versi:** 1.0 (Draft)
- **Arsitektur:** SPA + REST API; backend Modular Monolith
- **Stack:** Vue 3, TypeScript, Vite, Vue Router, Tailwind CSS, Axios, Laravel, MySQL

## 1. Prinsip Desain

1. Frontend dan backend adalah aplikasi berbeda dalam satu repositori.
2. REST API menjadi kontrak komunikasi.
3. Frontend dikelompokkan berdasarkan fitur; backend mengikuti struktur standar Laravel.
4. Komponen bersama dibuat ketika benar-benar generik dan digunakan lintas fitur.
5. Service layer digunakan saat logika bisnis perlu dipisahkan atau digunakan ulang; tidak diwajibkan untuk CRUD sederhana.
6. Pilih perubahan kecil, teruji, dan mudah ditinjau.
7. Gunakan Bahasa Indonesia untuk dokumentasi dan domain buatan sendiri, tetapi jangan menerjemahkan nama yang diwajibkan framework/tooling.

## 2. Gambaran Arsitektur

```text
┌──────────────────────────────────────────┐
│ Frontend: Vue 3 + TypeScript + Vite      │
│ Router, halaman, fitur, komponen bersama │
└───────────────────┬──────────────────────┘
                    │ HTTP/JSON
                    ▼
┌──────────────────────────────────────────┐
│ Backend: Laravel REST API /api/v1        │
│ Middleware → Form Request → Controller   │
│ → Service (jika perlu) → Model           │
│ → API Resource                           │
└───────────────────┬──────────────────────┘
                    │ Eloquent
                    ▼
┌──────────────────────────────────────────┐
│ MySQL                                    │
└──────────────────────────────────────────┘
```

Frontend tidak mengakses database secara langsung. Aturan bisnis dan otorisasi utama berada di backend.

## 3. Struktur Repositori

```text
universal-website-starter/
├── frontend/
├── backend/
├── docs/
│   ├── prd.md
│   ├── sdd/
│   │   ├── requirements.md
│   │   ├── design.md
│   │   └── tasks.md
│   └── steering/
│       ├── product.md
│       ├── structure.md
│       └── tech.md
├── .gitignore
└── README.md
```

Dokumen dapat diletakkan di lokasi lain jika tim menetapkan konvensi berbeda; yang penting konsisten.

## 4. Rancangan Frontend

```text
frontend/
├── public/
├── src/
│   ├── app/
│   │   ├── router/
│   │   │   ├── index.ts
│   │   │   └── routes.ts
│   │   ├── config/                            # Konstanta global: nama app, base URL API, batas pagination, dll
│   │   │   └── app.config.ts
│   │   └── providers/                         # Setup awal plugin/library: Pinia, i18n, toast provider, dll
│   ├── features/
│   │   ├── home/
│   │   │   └── pages/
│   │   │       └── HomePage.vue               # Landing page publik (Hero, Features, Tech stack, CTA)
│   │   ├── auth/
│   │   │   ├── pages/
│   │   │   │   └── LoginPage.vue
│   │   │   ├── components/
│   │   │   │   └── LoginForm.vue
│   │   │   ├── services/
│   │   │   │   └── authApi.ts
│   │   │   ├── composables/
│   │   │   │   └── useAuth.ts
│   │   │   └── types/
│   │   │       └── auth.types.ts
│   │   ├── dashboard/
│   │   │   ├── pages/
│   │   │   │   └── DashboardPage.vue
│   │   │   ├── components/
│   │   │   │   └── SummaryCard.vue
│   │   │   └── services/
│   │   ├── users/                             # Modul CRUD 1: Pengelolaan Pengguna (Sistem & Akun)
│   │   │   ├── pages/
│   │   │   │   ├── UserListPage.vue
│   │   │   │   ├── UserDetailPage.vue
│   │   │   │   └── UserFormPage.vue
│   │   │   ├── components/
│   │   │   │   ├── UserTable.vue
│   │   │   │   ├── UserFilterBar.vue
│   │   │   │   └── UserStatusBadge.vue
│   │   │   ├── services/
│   │   │   │   └── userApi.ts
│   │   │   ├── composables/
│   │   │   │   └── useUsers.ts
│   │   │   └── types/
│   │   │       └── user.types.ts
│   │   ├── posts/                             # Modul CRUD 2: Konten/Resource Bisnis (Relasi ke User, Status, Slug)
│   │   │   ├── pages/
│   │   │   │   ├── PostListPage.vue
│   │   │   │   ├── PostDetailPage.vue
│   │   │   │   └── PostFormPage.vue
│   │   │   ├── components/
│   │   │   │   ├── PostTable.vue
│   │   │   │   ├── PostFilterBar.vue
│   │   │   │   └── PostStatusBadge.vue
│   │   │   ├── services/
│   │   │   │   └── postApi.ts
│   │   │   ├── composables/
│   │   │   │   └── usePosts.ts
│   │   │   └── types/
│   │   │       └── post.types.ts
│   │   └── errors/                            # Halaman Penanganan Error
│   │       └── pages/
│   │           ├── NotFoundPage.vue           # Error 404
│   │           ├── ForbiddenPage.vue          # Error 403
│   │           └── ServerErrorPage.vue        # Error 500
│   ├── shared/                                # Komponen UI Bersama (Generik & Bebas Logika Bisnis)
│   │   ├── components/
│   │   │   ├── buttons/
│   │   │   │   ├── BaseButton.vue             # Tombol serbaguna (variants, sizes, loading, icon slots)
│   │   │   │   └── IconButton.vue             # Tombol khusus icon aksi tabel/header
│   │   │   ├── forms/
│   │   │   │   ├── FormField.vue              # Wrapper label, asterisk required, hint, pesan error
│   │   │   │   ├── BaseInput.vue              # Input teks, email, password, search, number
│   │   │   │   ├── BaseTextarea.vue           # Input teks multibaris dengan baris dinamis
│   │   │   │   ├── BaseSelect.vue             # Dropdown pemilihan opsi standar
│   │   │   │   ├── BaseCheckbox.vue           # Kotak centang boolean
│   │   │   │   └── BaseSwitch.vue             # Toggle switch aktif/nonaktif
│   │   │   ├── feedback/
│   │   │   │   ├── BaseAlert.vue              # Kotak pesan inline (info, success, warning, error)
│   │   │   │   ├── BaseToast.vue              # Floating flash toast notifikasi
│   │   │   │   ├── LoadingSpinner.vue         # Indikator pemuatan berputar
│   │   │   │   ├── EmptyState.vue             # Tampilan data kosong (icon, judul, teks, tombol aksi)
│   │   │   │   └── ErrorState.vue             # Tampilan kegagalan request/fetch dengan tombol coba lagi
│   │   │   ├── data/
│   │   │   │   ├── DataTable.vue              # Komponen tabel dinamis terstruktur dengan slot per-kolom
│   │   │   │   ├── Pagination.vue             # Kontrol navigasi halaman & per-page selector
│   │   │   │   ├── BaseBadge.vue              # Label status warna semantik (aktif, draft, sukses, dll)
│   │   │   │   └── BaseCard.vue               # Kontainer kartu berbingkai halus dengan header/body/footer
│   │   │   ├── overlays/
│   │   │   │   ├── BaseModal.vue              # Dialog modal dengan backdrop, escape key, focus trapping
│   │   │   │   ├── ConfirmDialog.vue          # Dialog konfirmasi aksi destruktif (hapus/nonaktifkan)
│   │   │   │   └── BaseDropdown.vue           # Popover menu aksi/profil
│   │   │   └── navigation/
│   │   │       └── Breadcrumbs.vue            # Navigasi jejak halaman (Home / Posts / Edit)
│   ├── layouts/
│   │   ├── AdminLayout.vue                    # Sidebar navigasi kiri + Top bar header + Konten utama responsif
│   │   ├── PublicLayout.vue                   # Top navigation bar + Konten container + Footer
│   │   └── AuthLayout.vue                     # Layout kartu tengah terisolasi untuk login/auth
│   ├── services/
│   │   └── api/
│   │       ├── client.ts                      # Konfigurasi instance Axios terpusat
│   │       └── interceptors.ts                # Interceptor otomatis token/CSRF dan penanganan error HTTP
│   ├── utils/
│   │   ├── formatters.ts                      # Format tanggal, angka, teks
│   │   └── validators.ts                      # Helper validasi ringan frontend
│   ├── types/
│   │   ├── api.types.ts                       # Tipe standar ApiResponse, ApiError, PaginatedMeta
│   │   └── common.types.ts                    # Tipe umum (SortOrder, SelectOption, TableColumn)
│   ├── styles/
│   │   └── main.css                           # Setup Tailwind CSS directives & CSS utility dasar
│   ├── App.vue
│   └── main.ts
├── .env.example
├── package.json
├── tsconfig.json
└── vite.config.ts
```

### Aturan Frontend

- `features/`: Kode spesifik fitur (halaman, komponen privat, composable, tipe data) berada dalam folder fitur terkait.
- `shared/`: Komponen UI murni yang bebas dari aturan bisnis spesifik dan dapat digunakan di semua fitur.
- `layouts/`: Membungkus kerangka tata letak visual (`AdminLayout` dengan sidebar kiri, `PublicLayout` dengan top bar, `AuthLayout` untuk form terisolasi).
- `services/api/`: Konfigurasi terpusat HTTP client Axios; semua request melalui layer ini dengan error interceptor konsisten.
- `app/router/`: Konfigurasi rute, guard otentikasi/otorisasi, dan rute catch-all untuk halaman error 404.
- `types/`: Tipe global bersama (`api.types.ts`, `common.types.ts`). Tipe data milik domain (misal `user.types.ts` dan `post.types.ts`) disimpan di folder fitur masing-masing.
- Hindari pembuatan folder kosong atau barrel file (`index.ts`) berlebihan yang hanya meneruskan re-export tanpa fungsi nyata.

## 5. Rancangan Backend Laravel

```text
backend/
├── app/
│   ├── Http/
│   │   ├── Controllers/Api/V1/
│   │   │   ├── AuthController.php       # login, logout, me
│   │   │   ├── UserController.php       # CRUD Pengguna (Modul 1)
│   │   │   └── PostController.php       # CRUD Post/Artikel (Modul 2 - Relasi & Status)
│   │   ├── Requests/
│   │   │   ├── Auth/
│   │   │   │   └── LoginRequest.php
│   │   │   ├── User/
│   │   │   │   ├── StoreUserRequest.php
│   │   │   │   └── UpdateUserRequest.php
│   │   │   └── Post/
│   │   │       ├── StorePostRequest.php
│   │   │       └── UpdatePostRequest.php
│   │   ├── Resources/
│   │   │   ├── UserResource.php
│   │   │   └── PostResource.php
│   │   └── Middleware/
│   ├── Models/
│   │   ├── User.php
│   │   └── Post.php                     # BelongsTo User (author_id)
│   ├── Policies/
│   │   ├── UserPolicy.php
│   │   └── PostPolicy.php
│   └── Services/                        # Opsional, dibuat saat logika bisnis memerlukan isolasi
├── database/
│   ├── factories/
│   │   ├── UserFactory.php
│   │   └── PostFactory.php
│   ├── migrations/
│   │   ├── xxxx_create_users_table.php
│   │   └── xxxx_create_posts_table.php  # title, slug, content, status (draft/published), author_id
│   └── seeders/
│       ├── DatabaseSeeder.php
│       ├── UserSeeder.php
│       └── PostSeeder.php
├── routes/
│   └── api.php                          # Rute /api/v1/auth, /api/v1/users, /api/v1/posts
├── tests/
│   ├── Feature/
│   │   ├── AuthTest.php
│   │   ├── UserCrudTest.php
│   │   └── PostCrudTest.php
│   └── Unit/
├── .env.example
└── composer.json
```

### Tanggung jawab lapisan

- **Controller:** menerima permintaan HTTP, mengoordinasikan alur, dan mengembalikan respons JSON standar.
- **Form Request:** validasi input dan otorisasi tingkat permintaan sebelum controller dieksekusi.
- **Model:** relasi dan akses data melalui Eloquent (`Post` berelasi `User` via `author_id`).
- **Policy:** aturan otorisasi sumber daya (contoh: hanya admin yang dapat mengubah user lain; hanya author/admin yang dapat mengubah post).
- **Service:** logika bisnis yang kompleks, berulang, atau perlu dipisahkan dari controller.
- **API Resource:** membentuk representasi JSON yang stabil dan konsisten.
- **Migration/Seeder/Factory:** perubahan skema dan data pengembangan/pengujian.

## 6. Kontrak API

Gunakan bahasa Inggris standar untuk nama resource dan endpoint API.

### Endpoint Autentikasi
- `POST /api/v1/auth/login`
- `POST /api/v1/auth/logout`
- `GET  /api/v1/auth/me`

### Endpoint Modul 1 — Users (Pengelolaan Pengguna)
- `GET    /api/v1/users` (Mendukung query `page`, `per_page`, `search`, `role`, `status`)
- `POST   /api/v1/users`
- `GET    /api/v1/users/{id}`
- `PUT    /api/v1/users/{id}`
- `DELETE /api/v1/users/{id}`

### Endpoint Modul 2 — Posts (Contoh Resource Bisnis / Konten)
- `GET    /api/v1/posts` (Mendukung query `page`, `per_page`, `search`, `status`, `author_id`)
- `POST   /api/v1/posts`
- `GET    /api/v1/posts/{id}`
- `PUT    /api/v1/posts/{id}`
- `DELETE /api/v1/posts/{id}`

### Respons sukses contoh
```json
{
  "success": true,
  "data": {
    "id": 1,
    "name": "Admin System",
    "email": "admin@example.com",
    "role": "admin"
  },
  "message": "Operasi berhasil."
}
```

### Respons daftar contoh (Pagination)
```json
{
  "data": [
    {
      "id": 1,
      "title": "Memulai dengan Template Web",
      "slug": "memulai-dengan-template-web",
      "status": "published",
      "author": {
        "id": 1,
        "name": "Admin System"
      },
      "created_at": "2026-10-27T00:00:00.000000Z"
    }
  ],
  "meta": {
    "current_page": 1,
    "per_page": 10,
    "total": 1,
    "last_page": 1
  }
}
```

### Respons kesalahan validasi (422)
```json
{
  "message": "Data yang dikirim tidak valid.",
  "errors": {
    "email": ["Format email tidak valid."]
  }
}
```

### Respons kesalahan akses & server (401, 403, 404, 500)
```json
{
  "message": "Akses tidak diizinkan atau sesi telah kedaluwarsa."
}
```

## 7. Autentikasi dan Keamanan

- Gunakan Laravel Sanctum.
- Untuk SPA pihak pertama, gunakan cookie/sesi dengan konfigurasi stateful domain, CORS, dan CSRF yang benar.
- Untuk klien mobile atau klien token, gunakan token Sanctum bila dibutuhkan.
- Jangan commit kredensial, private key, atau rahasia.
- Jangan menjadikan `localStorage` tempat default token sensitif.
- Backend wajib memeriksa autentikasi dan otorisasi pada setiap endpoint privat.
- Gunakan throttling untuk login dan endpoint yang sesuai.
- Jangan mencatat kata sandi, token, atau data sensitif ke log.
- Gunakan HTTPS pada deployment.
- Atur CORS secara eksplisit; hindari wildcard ketika memakai kredensial.
- Perubahan skema dilakukan melalui migration.

## 8. Rancangan Antarmuka

### Arah Visual & Desain Sistem
- Tema terang (Light mode) yang bersih, modern, dan profesional dengan rasio kontras tinggi.
- Palet warna: Slate/Gray netral untuk teks dan latar, Indigo/Blue sebagai aksen utama, Emerald untuk status sukses, Amber untuk peringatan, Rose/Red untuk bahaya/destruktif.
- Radius konsisten (`rounded-lg`), bayangan halus (`shadow-sm` hingga `shadow-md`), garis tepi subtil (`border border-slate-200`).
- Tipografi modern dan bersih (Inter / sans-serif sistem).

### Tata Letak Inti

1. **AdminLayout (`layouts/AdminLayout.vue`)**
   - **Sidebar Kiri:**
     - Header sidebar dengan nama/logo aplikasi.
     - Navigasi menu terstruktur dengan icon dan indikator tautan aktif.
     - Menu: Dashboard, Users Management, Posts Management, Pengaturan.
     - Responsif: Di desktop selalu terlihat atau dapat diciutkan (collapsible); di perangkat mobile (< 1024px) menjadi drawer overlay dengan animasi transisi mulus dan tombol penutup/backdrop.
   - **Top Header:**
     - Tombol toggle sidebar hamburger untuk mobile/desktop.
     - Navigasi Breadcrumbs terintegrasi.
     - Dropdown profil pengguna (avatar, nama, tombol edit profil, tombol logout).
   - **Area Konten:**
     - Container dengan padding adaptif (`p-4 md:p-6 lg:p-8`), scroll independen, dan header judul halaman dengan slot tombol aksi utama.

2. **PublicLayout (`layouts/PublicLayout.vue`)**
   - **Top Navigation Bar:**
     - Sticky top navbar dengan latar semi-transparan ber-blur (`backdrop-blur-md bg-white/90`).
     - Sisi kiri: Logo dan nama aplikasi.
     - Sisi tengah: Menu navigasi publik (Home, Fitur, Teknologi, Dokumentasi).
     - Sisi kanan: Tombol CTA "Masuk" / "Buka Dashboard" (bergantung status login).
   - **Area Konten Utama:**
     - Kontainer terpusat untuk halaman Home/Landing Page atau halaman publik lainnya.
   - **Footer Publik:**
     - Informasi hak cipta, link navigasi cepat, dan identitas proyek starter template.

3. **AuthLayout (`layouts/AuthLayout.vue`)**
   - Halaman terpusat (centered card) dengan latar netral bersih, logo aplikasi, judul form login, alert error sesi/kredensial, dan link kembali ke Home.

### Desain Halaman Error

Halaman error menggunakan tata letak ramah pengguna dengan pesan yang informatif dan opsi pemulihan yang jelas:

1. **404 — Not Found (`features/errors/pages/NotFoundPage.vue`)**
   - **Konteks:** Rute atau data yang diminta tidak ditemukan oleh Vue Router atau API.
   - **Visual:** Badge kode status `404`, icon ilustrasi pencarian/peta kosong.
   - **Judul:** "Halaman Tidak Ditemukan"
   - **Deskripsi:** "Maaf, halaman yang Anda cari tidak ada atau mungkin telah dipindahkan."
   - **Aksi:** Tombol primer "Kembali ke Beranda" (link ke `/`) dan tombol sekunder "Buka Dashboard" (link ke `/dashboard`).

2. **403 — Forbidden (`features/errors/pages/ForbiddenPage.vue`)**
   - **Konteks:** Pengguna mencoba membuka halaman atau melakukan tindakan yang melampaui peran/hak aksesnya.
   - **Visual:** Badge kode status `403`, icon gembok atau perisai keamanan dengan aksen peringatan.
   - **Judul:** "Akses Dibatasi"
   - **Deskripsi:** "Anda tidak memiliki izin yang cukup untuk mengakses halaman atau sumber daya ini."
   - **Aksi:** Tombol primer "Kembali ke Halaman Sebelumnya" (`router.back()`) dan tombol sekunder "Ke Dashboard".

3. **500 — Server Error (`features/errors/pages/ServerErrorPage.vue`)**
   - **Konteks:** Terjadi kesalahan internal tak terduga pada backend server.
   - **Visual:** Badge kode status `500`, icon peringatan teknis server.
   - **Judul:** "Terjadi Kesalahan Server"
   - **Deskripsi:** "Server kami sedang mengalami gangguan internal. Tim teknis sedang menanganinya. Silakan coba beberapa saat lagi."
   - **Aksi:** Tombol primer "Muat Ulang Halaman" (`window.location.reload()`) dan tombol sekunder "Kembali ke Beranda".

### Penanganan Keadaan UI (States)
Setiap halaman daftar atau formulir wajib menangani 5 keadaan:
1. **Loading State:** Skeleton loader atau spinner halus pada tabel/tombol.
2. **Empty State:** Komponen `EmptyState.vue` ketika data 0 hasil pencarian atau belum ada data.
3. **Error State:** Komponen `ErrorState.vue` dengan pesan yang ramah dan tombol "Coba Lagi".
4. **Success State:** Toast notifikasi hijau yang muncul mengambang dan otomatis hilang dalam 3 detik.
5. **Validation State:** Pesan error per-field dari server (422) ditampilkan di bawah masing-masing input.

## 9. Konvensi Penamaan

- Komponen Vue menggunakan format `PascalCase.vue` (contoh: `BaseButton.vue`, `UserTable.vue`).
- Fungsi, variabel, composable, dan modul TypeScript menggunakan format `camelCase` secara konsisten (contoh: `useAuth.ts`, `userApi.ts`, `formatDate()`).
- File deklarasi tipe data TypeScript menggunakan akhiran `.types.ts` (contoh: `user.types.ts`, `api.types.ts`).
- Kelas PHP menggunakan format `PascalCase` (contoh: `UserController`, `PostPolicy`); method menggunakan `camelCase` sesuai standar PSR-12 dan konvensi resmi Laravel.
- Nama tabel database MySQL menggunakan format jamak huruf kecil `snake_case` (contoh: `users`, `posts`); kunci asing (*foreign key*) menggunakan format `nama_tabel_tunggal_id` (contoh: `author_id`, `user_id`).
- Berkas dan direktori bawaan framework Laravel/Vue tetap mempertahankan konvensi resmi bawaan masing-masing framework.
- Hindari singkatan yang tidak jelas serta penamaan samar seperti `data2`, `helperFinal`, atau `CommonManager` yang tidak memiliki makna spesifik.
- Gunakan satu istilah entitas domain yang konsisten di seluruh aplikasi (contoh: selalu gunakan istilah `user`, jangan mencampuradukkan dengan `member` atau `account` untuk merujuk pada objek yang sama).
- Seluruh dokumentasi proyek ditulis dalam Bahasa Indonesia untuk memastikan pemahaman yang jelas bagi seluruh tim pengembang.

## 10. Pengujian

### Backend
- Feature test untuk login/logout, endpoint privat, otorisasi, validasi, dan CRUD pengguna.
- Feature test untuk CRUD posts (validasi status, slug, relasi author, otorisasi policy).
- Gunakan factory dan database pengujian yang terisolasi.

### Frontend
- Uji alur rute dan auth guards (tamu diarahkan ke login, pengguna login diarahkan ke dashboard).
- Uji alur CRUD form validasi dan tabel.
- Minimal jalankan pemeriksaan tipe TypeScript (`vue-tsc --noEmit`) dan build produksi (`vite build`).

### Pemeriksaan sebelum selesai
- Tes yang relevan lulus.
- Lint/type-check/build lulus sesuai konfigurasi.
- Tidak ada regresi yang diketahui.
- Dokumentasi diperbarui jika pola atau kontrak berubah.

## 11. Status Keputusan

- **Bahasa & Dialek Frontend:** TypeScript (Aktif).
- **CSS Framework:** Tailwind CSS (Aktif).
- **Tema:** Light mode bersih dan profesional (Dark mode dilewati/skip untuk menjaga fokus MVP).
- **Halaman Publik:** Halaman Home/Landing page dengan `PublicLayout` (Top Navigation) (Aktif).
- **Tata Letak Admin:** `AdminLayout` dengan Sidebar kiri responsif (Aktif).
- **Modul CRUD Acuan:** Dua modul lengkap: (1) `users` (manajemen akun & sistem) dan (2) `posts` (manajemen konten bisnis dengan relasi & status) (Aktif).
- **Keputusan Ditunda Pasca-MVP:**
  - Dark mode switcher.
  - Multi-tenant / Multi-bahasa (i18n).
  - Ekspor data (PDF/Excel/CSV).
  - Notifikasi real-time WebSocket.
