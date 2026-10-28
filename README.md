# Universal Website Starter Template

Template full-stack yang dapat digunakan ulang sebagai fondasi berbagai proyek website. Berisi struktur, autentikasi, pengelolaan pengguna, komponen UI, pola CRUD, dan panduan pengembangan.

**Stack:** Vue 3 + TypeScript + Vite · Laravel REST API · MySQL · Laravel Sanctum

---

## Struktur Dokumentasi

```text
Template Web/
│
├── README.md                  ← Dokumen ini
│
└── docs/                      ← Semua dokumentasi proyek
    ├── prd.md                 ← Tujuan produk, scope, kebutuhan, dan kriteria MVP
    ├── sdd/                   ← Spec-Driven Development
    │   ├── requirements.md    ← Kebutuhan fungsional & nonfungsional
    │   ├── design.md          ← Arsitektur, struktur folder, kontrak API, UI, pengujian
    │   └── tasks.md           ← Tahapan implementasi dan checklist
    └── steering/              ← Aturan pengembangan berkelanjutan
        ├── product.md         ← Misi, prioritas, batasan, dan definisi selesai produk
        ├── structure.md       ← Aturan struktur folder, reuse, dan penamaan
        └── tech.md            ← Stack, standar API, keamanan, Git, dan checklist selesai
```

---

## Urutan Membaca

1. **`prd.md`** — Pahami tujuan, scope MVP, dan prinsip produk sebelum mulai.
2. **`sdd/requirements.md`** — Pastikan apa yang wajib dibangun dan kriteria penerimaannya.
3. **`sdd/design.md`** — Pahami arsitektur dan struktur sebelum mengubah atau menambah kode.
4. **`sdd/tasks.md`** — Ikuti tahapan implementasi; kerjakan satu irisan kecil pada satu waktu.
5. **`steering/`** — Patuhi aturan ini sepanjang seluruh pengembangan.

---

## Alur Pengembangan (SDD)

Setiap fitur dikerjakan dengan urutan berikut:

1. **Requirements** — tulis kebutuhan, aktor, alur, dan kriteria penerimaan.
2. **Design** — jelaskan struktur, kontrak API, perubahan database, dan keamanan.
3. **Tasks** — pecah menjadi tugas kecil yang dapat diverifikasi.
4. **Implementasi** — kerjakan bertahap; cari yang sudah ada sebelum membuat baru.
5. **Verifikasi** — jalankan tes, type-check, dan build.
6. **Dokumentasi** — perbarui dokumen yang terpengaruh.

---

## Catatan Penting

- Jangan membuat folder atau file kosong tanpa kebutuhan nyata.
- Cari implementasi yang sudah ada sebelum membuat yang baru.
- Rahasia dan file hasil build tidak boleh masuk repositori.
- Ikuti konvensi Laravel dan Vue; jangan menerjemahkan nama yang diwajibkan framework.
- Verifikasi versi dependency saat bootstrap proyek.
