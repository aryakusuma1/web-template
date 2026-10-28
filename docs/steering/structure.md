# Steering — Structure

## 1. Prinsip Struktur

- Kelompokkan kode berdasarkan tanggung jawab dan fitur.
- Pisahkan frontend dan backend di tingkat repositori.
- Pertahankan konvensi resmi Vue/Vite dan Laravel.
- Buat folder saat ada kode yang perlu ditempatkan di dalamnya, bukan untuk mengisi struktur kosong.

## 2. Aturan Frontend

- Halaman, komponen, tipe, dan layanan spesifik berada di folder fitur terkait.
- `shared/` berisi UI lintas fitur yang tidak bergantung pada aturan bisnis tertentu.
- `layouts/` menampung kerangka visual lintas halaman, bukan logika bisnis.
- Permintaan HTTP melewati API client terpusat.
- Utilitas dan tipe global hanya berisi hal yang benar-benar dipakai lintas fitur.
- Hindari file barrel/index yang hanya meneruskan ekspor tanpa manfaat nyata.
- Gunakan Pinia jika state memang perlu dibagikan lintas komponen/fitur.

## 3. Aturan Backend

- Route memetakan endpoint; Controller mengorkestrasi HTTP.
- Gunakan Form Request untuk validasi request yang sesuai.
- Gunakan API Resource untuk representasi data konsisten bila sesuai.
- Gunakan Policy/middleware untuk otorisasi.
- Gunakan Model/Eloquent mengikuti pola Laravel.
- Buat Service jika proses bisnis kompleks, digunakan ulang, atau lebih mudah diuji terpisah.
- Jangan otomatis membuat Repository, Interface, BaseController, Manager, atau lapisan tambahan untuk setiap fitur.

## 4. Aturan Reuse

1. Cari komponen, layanan, tipe, dan pola yang sudah ada.
2. Evaluasi apakah kebutuhan baru benar-benar sama dengan kebutuhan lama.
3. Jika sesuai, gunakan/perluas implementasi tanpa merusak perilaku lama.
4. Jika tanggung jawab berbeda, buat implementasi baru dengan nama spesifik.
5. Tambahkan pengujian untuk perilaku baru dan perilaku lama yang mungkin terdampak.

## 5. Penamaan dan Konvensi

- Gunakan konvensi standar masing-masing framework: komponen Vue `PascalCase`; variabel/fungsi TypeScript `camelCase`; kelas PHP `PascalCase` mengikuti konvensi Laravel.
- Gunakan istilah domain yang konsisten dan hindari nama samar seperti `data`, `manager`, `common`, atau `helper` jika nama yang lebih spesifik tersedia.
- Komentar menjelaskan alasan atau perilaku non-obvious, bukan mengulang kode.
- Dokumentasi boleh ditulis dalam Bahasa Indonesia untuk kejelasan.

## 6. Hindari

- Menyalin seluruh halaman hanya untuk perbedaan kecil.
- Komponen generik dengan terlalu banyak prop dan kondisi.
- Logika bisnis tersebar di komponen UI.
- Folder utilitas sebagai tempat penampungan semua fungsi.
- Perubahan struktur besar tanpa kebutuhan atau rencana migrasi yang jelas.
