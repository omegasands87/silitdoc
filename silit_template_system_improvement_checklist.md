# SILIT — Checklist Khusus Sistem Template yang Dapat Diedit

**Status:** Rencana kerja khusus — belum diverifikasi/diimplementasikan seluruhnya  
**Repository kode:** `omegasands87/silit`  
**Repository dokumentasi:** `omegasands87/silitdoc`  
**Branch:** `main`  
**Dokumen utama yang tetap mengikat:** `silit_ai_mandatory_rules.md`, `silit_visual_editor_checklist.md`, `silit_uiux_reference_guide.md`, dan `silit_source_code_findings_deferred.md`.

---

## 1. Tujuan

Membangun sistem template SILIT yang memungkinkan pengguna memilih template ketika menambahkan halaman baru, lalu mengedit komponen template secara individual melalui editor yang sama.

Template dapat memiliki komposisi, jumlah, jenis, urutan, dan layout elemen yang berbeda. Sistem tidak boleh mengharuskan semua template memakai susunan elemen Classic.

Target awal:
- Mempertahankan template Classic yang sudah ada dan kemampuan editnya.
- Mengintegrasikan template Cover `Double Smash Cheeseburger` dari HTML yang diberikan.
- Menyediakan alur pemilihan template setelah pengguna memilih jenis halaman.
- Membuat komponen utama template baru dapat dipilih dan diedit secara individual.
- Mempertahankan urutan halaman, operasi halaman, ukuran A4, dan kesesuaian export.
- Menyiapkan pola yang dapat digunakan untuk menambah template berikutnya tanpa menulis ulang sistem editor.

Dokumen ini adalah checklist turunan khusus. Dokumen ini **tidak mengganti, mengurangi, menulis ulang, atau mengubah urutan** checklist utama.

## 2. Keputusan Owner yang Sudah Ditetapkan

1. Prioritas visual template baru adalah mempertahankan desain HTML sumber sedekat mungkin dengan tampilan referensi.
2. Elemen utama template baru harus dapat dipilih dan diedit secara terpisah.
3. Classic dan template baru sama-sama harus bisa diedit melalui sistem editor SILIT.
4. Setiap template boleh mempunyai komposisi dan jumlah komponen berbeda.
5. Pemilihan template dilakukan setelah pengguna memilih jenis halaman pada alur Tambah Halaman.
6. Halaman baru secara default ditambahkan di akhir urutan dokumen yang sedang ada. Penomoran harus mengikuti posisi aktual halaman.
7. Template yang dipilih menjadi dasar halaman baru; perubahan pada halaman tidak boleh mengubah template sumber atau halaman lain.
8. Isi dan Langkah Memasak tetap menggunakan pilihan yang tersedia untuk jenis masing-masing. Jangan menampilkan template yang belum benar-benar tersedia.
9. Backend, database, Supabase, Cloudflare R2, persistence, dan layanan penyimpanan lain tidak termasuk scope.
10. Tidak ada deployment oleh AI.

## 3. Batasan dan Aturan Perubahan

### 3.1 Dokumen dan checklist

- Jangan mengubah teks, urutan, acceptance criteria, atau scope pada checklist utama.
- Jangan mengubah isi dokumen wajib atau dokumen referensi.
- Pada dokumen checklist, satu-satunya perubahan progres yang diperbolehkan setelah dokumen ini dibuat adalah mengubah status kotak checklist `[ ]` menjadi `[x]` setelah kriteria item benar-benar terpenuhi dan terverifikasi.
- Jangan mencentang item berdasarkan niat, pembacaan kode saja, atau klaim yang belum diuji.
- Jika ada requirement baru, jangan menambahkannya diam-diam ke checklist. Hentikan pekerjaan, jelaskan dampak, dan minta persetujuan owner.

### 3.2 Kode aplikasi

- Perubahan kode hanya boleh mengikuti scope dan urutan kerja yang disetujui dalam dokumen ini dan checklist utama.
- Jangan melakukan refactor umum atau memperbaiki temuan source code lain yang tidak dibutuhkan langsung oleh scope ini.
- Jangan menghapus atau mengganti fitur editor yang sudah ada.
- Jangan mengganti gambar, font, warna, teks, ukuran, crop, komposisi, atau aset asli template Double Smash dengan aset buatan ulang.
- Jangan menggunakan screenshot atau satu gambar datar sebagai pengganti komponen yang harus dapat diedit.
- Jangan mengklaim kesamaan visual mutlak sebelum dibandingkan pada kondisi render yang sama.
- Jangan menambahkan backend, database, Supabase, R2, atau persistence.
- Jangan deploy.

### 3.3 Ketergantungan dengan checklist utama

Checklist utama tetap menjadi urutan dan batas kerja utama. Checklist khusus ini tidak memberi izin untuk melewati tahapan utama yang belum selesai. Sebelum mengerjakan tahap khusus, periksa checklist utama dan pastikan prasyarat editor yang terkait sudah lulus. Jika ada konflik atau perubahan di luar scope, berhenti dan minta persetujuan.

## 4. Arsitektur Target

Sistem dibagi menjadi tiga tanggung jawab konseptual:

1. **Editor bersama:** selection, drag, resize, panel KONTEN/DESAIN, layer, undo/redo, zoom, page management, dan export.
2. **Definisi elemen template:** identitas stabil, jenis elemen, data awal, posisi, ukuran, urutan layer, properti visual, dan aturan kemampuan edit.
3. **Layout/renderer template:** komposisi yang berbeda untuk setiap template, menggunakan definisi elemen yang tetap kompatibel dengan editor bersama.

Tidak wajib semua template menggunakan komponen visual yang sama. Namun, setiap komponen yang dinyatakan dapat diedit harus terhubung ke model elemen editor, mempunyai identitas stabil, dan dapat diperbarui tanpa merusak elemen lain.

Renderer khusus diperbolehkan hanya jika dibutuhkan untuk mempertahankan layout kompleks. Renderer tersebut tetap harus mengekspos komponen yang dapat diedit ke kontrak editor bersama. HTML yang hanya ditampilkan dalam iframe tanpa sinkronisasi ke model elemen tidak memenuhi target akhir editabilitas penuh.

## 5. Tahap Kerja dan Checklist

Semua item dimulai belum dicentang. Centang hanya setelah implementasi dan verifikasi nyata.

### Tahap 0 — Baseline dan pemeriksaan scope

- [x] Baca ulang semua dokumen wajib yang masih berlaku.
- [x] Periksa ulang branch `main` dan source code terbaru; jangan mengandalkan line number atau ringkasan lama.
- [x] Catat kondisi awal Add Page, Duplicate Page, Delete Page, Move Page, selection, editor Classic, undo/redo, dan export.
- [x] Periksa implementasi HTML Cover yang sudah ada dan identifikasi bagian yang hanya visual statis/iframe.
- [x] Pastikan tidak ada perubahan tak terkait yang akan ikut dikerjakan.
- [x] Pastikan urutan checklist utama tetap dipatuhi.

**Lulus jika:** baseline ditulis berdasarkan source/runtime yang benar-benar diperiksa, risiko dan batas pengujian jelas, serta tidak ada scope creep.

### Tahap 1 — Kontrak template dan elemen

- [ ] Tetapkan representasi data template yang dapat memiliki jumlah dan tipe elemen berbeda.
- [ ] Setiap elemen mempunyai ID stabil yang tidak bergantung pada posisi array.
- [ ] Definisikan tipe elemen yang diperlukan oleh sumber template awal: teks, gambar, dan elemen dekoratif/shape bila memang ditemukan pada HTML.
- [ ] Definisikan data awal, posisi, ukuran, layer, tipografi, warna, alignment, dan properti visual yang dibutuhkan.
- [ ] Tentukan properti mana yang dapat diedit melalui KONTEN dan mana melalui DESAIN.
- [ ] Tentukan bagaimana template default dibuat menjadi data halaman baru yang independen.
- [ ] Pastikan definisi template tidak memodifikasi data halaman lain.

**Lulus jika:** kontrak mendukung komposisi template berbeda tanpa kondisi khusus yang mengunci editor pada struktur Classic.

### Tahap 2 — Alur Tambah Halaman dan pemilihan template

- [ ] Klik Tambah Halaman menampilkan pilihan jenis: Cover, Isi, dan Langkah Memasak.
- [ ] Memilih jenis halaman membuka dialog/popup pemilihan template yang sesuai jenisnya.
- [ ] Popup hanya menampilkan template yang benar-benar tersedia untuk jenis tersebut.
- [ ] Cover menyediakan Classic dan Double Smash Cheeseburger selama keduanya terdaftar dan valid.
- [ ] Isi dan Langkah Memasak tetap menyediakan Classic; jangan membuat template baru untuk jenis tersebut tanpa sumber/approval.
- [ ] Pengguna dapat membatalkan popup tanpa menambah halaman.
- [ ] Memilih template membuat tepat satu halaman baru.
- [ ] Halaman baru secara default ditambahkan di akhir urutan dokumen.
- [ ] Nomor halaman dan label template mencerminkan urutan dan template yang sebenarnya.
- [ ] Add Page tidak mengubah atau menghapus halaman yang sudah ada.

**Lulus jika:** alur jenis halaman → popup template → halaman baru bekerja konsisten dan tidak mengubah urutan/data halaman yang sudah ada.

### Tahap 3 — Data halaman dan isolasi template

- [ ] Template menjadi sumber nilai awal, bukan referensi bersama yang ikut berubah ketika halaman diedit.
- [ ] Mengedit teks di halaman hasil template tidak mengubah halaman lain.
- [ ] Mengganti gambar di halaman hasil template tidak mengubah halaman lain.
- [ ] Mengubah posisi, ukuran, atau gaya elemen tidak mengubah template sumber.
- [ ] Duplicate Page mempertahankan data dan template halaman sumber sesuai perilaku duplikasi yang disetujui.
- [ ] Delete Page dan Move Page tetap berfungsi untuk semua template.
- [ ] Undo/redo mencatat perubahan halaman/elemen dengan benar sesuai aturan history pada checklist utama.

**Lulus jika:** halaman dari template yang sama dapat diedit secara independen dan operasi halaman tetap aman.

### Tahap 4 — Editabilitas Classic tanpa regresi

- [ ] Pastikan seluruh komponen Classic yang saat ini dapat diedit tetap dapat diedit.
- [ ] Selection dan panel KONTEN bekerja untuk elemen Classic.
- [ ] Panel DESAIN tetap mengubah elemen Classic yang dipilih.
- [ ] Layer, drag, resize, alignment, guides/snap, multi-select, dan keyboard shortcut tidak mengalami regresi.
- [ ] Upload/ganti gambar tetap bekerja.
- [ ] Undo/redo tetap bekerja untuk operasi yang didukung.
- [ ] Export dan print template Classic tetap sesuai checklist utama.

**Lulus jika:** tidak ada penurunan fungsi Classic akibat sistem template baru. Item ini tidak boleh dicentang hanya karena UI terlihat benar; lakukan pengujian interaksi.

### Tahap 5 — Adaptasi HTML Cover menjadi elemen editor

- [ ] Periksa ulang HTML asli dan identifikasi semua bagian visual, aset, font tertanam, CSS, dan efeknya.
- [ ] Pertahankan aset gambar burger dan font asli; jangan mengganti dengan gambar/font pengganti.
- [ ] Petakan label kategori, judul, subtitle/deskripsi, informasi waktu, informasi persiapan/memasak, kalori, porsi, dan gambar burger ke elemen yang sesuai berdasarkan HTML aktual.
- [ ] Identifikasi teks dekoratif/shape/garis yang perlu direpresentasikan agar komposisi tetap setia.
- [ ] Setiap elemen yang dijanjikan dapat diedit mempunyai ID stabil dan dapat dipilih.
- [ ] Judul, subtitle, gambar, waktu, dan teks informasi/footer dapat dipilih satu per satu.
- [ ] Panel KONTEN mengubah nilai konten elemen yang sesuai.
- [ ] Panel DESAIN mengubah properti visual yang didukung untuk elemen yang dipilih.
- [ ] Panel LAYER menampilkan elemen template yang memang dapat dipilih dan memungkinkan operasi layer yang didukung.
- [ ] Drag dan resize bekerja pada elemen yang kompatibel tanpa memisahkan posisi visual dari posisi editor.
- [ ] Perubahan elemen tidak menyebabkan layout elemen lain rusak tanpa aturan yang disengaja.
- [ ] Hapus atau nonaktifkan jalur iframe statis hanya setelah renderer berbasis elemen terverifikasi setara; jangan menghapus fallback lebih awal jika masih diperlukan untuk pengembangan.
- [ ] Tidak ada penggantian diam-diam terhadap warna, font, crop, proporsi, atau aset asli.

**Lulus jika:** komponen utama Cover dapat diedit secara individual melalui editor dan tampilan tetap cocok dengan HTML sumber dalam batas verifikasi yang ditetapkan.

### Tahap 6 — Fidelity visual Cover

- [ ] Tetapkan kondisi perbandingan yang sama: ukuran A4, viewport/zoom, font siap dimuat, dan kondisi render.
- [ ] Bandingkan ukuran halaman 210 mm × 297 mm.
- [ ] Bandingkan gradasi dan warna latar.
- [ ] Bandingkan keluarga font, bobot, ukuran, line-height, letter-spacing, dan italic.
- [ ] Bandingkan posisi, jarak, alignment, dan proporsi semua komponen.
- [ ] Bandingkan gambar burger, ukuran, crop, transparansi, dan bayangan.
- [ ] Bandingkan garis dekoratif, footer, dan margin.
- [ ] Perbaiki hanya perbedaan yang terkait dengan template ini dan scope yang disetujui.
- [ ] Catat perbedaan yang belum dapat dihilangkan; jangan mengklaim identik jika belum terbukti.

**Lulus jika:** perbandingan visual dilakukan pada kondisi render setara, tidak ada perbedaan yang tidak dijelaskan, dan hasil memenuhi target owner sejauh dapat diverifikasi.

### Tahap 7 — A4, print/export, dan pagination

- [ ] Pastikan halaman template mempunyai ukuran A4 yang sama dengan template Classic.
- [ ] Pastikan penambahan halaman tidak menyebabkan nomor/urutan halaman salah.
- [ ] Uji export halaman saat ini untuk template Classic.
- [ ] Uji export halaman saat ini untuk template Double Smash.
- [ ] Uji export semua halaman dengan campuran Classic dan Double Smash.
- [ ] Pastikan tidak ada UI editor di hasil print/PDF.
- [ ] Bandingkan font, warna, gambar, crop, layer, posisi, ukuran, dan margin antara canvas dan hasil print/PDF.
- [ ] Pastikan tidak ada halaman kosong tambahan atau pemotongan konten.
- [ ] Periksa perilaku iframe/renderer ketika print; jika hasil tidak konsisten, gunakan solusi render yang kompatibel dan tetap mempertahankan elemen editable.
- [ ] Jangan mengganti pendekatan export secara luas tanpa persetujuan jika perubahan melewati scope checklist utama.

**Lulus jika:** export memenuhi kriteria yang relevan pada checklist utama dan template baru tidak merusak export halaman lain.

### Tahap 8 — Regression test dan Definition of Done khusus template

- [ ] Uji Add Page untuk masing-masing jenis halaman.
- [ ] Uji pemilihan Classic dan Double Smash pada Cover.
- [ ] Uji batal pada popup template.
- [ ] Uji tambah halaman berulang kali dan pastikan urutan/nomor benar.
- [ ] Uji selection setiap elemen utama Cover.
- [ ] Uji edit konten dan gaya setiap elemen utama Cover.
- [ ] Uji ganti gambar burger dan pastikan aset tidak rusak.
- [ ] Uji layer, drag, resize, undo, dan redo.
- [ ] Uji Duplicate Page, Move Page, dan Delete Page pada halaman template baru.
- [ ] Uji bahwa halaman Classic yang sudah ada tidak berubah.
- [ ] Uji canvas, zoom, dan print/export.
- [ ] Periksa runtime error di browser.
- [ ] Catat lingkungan, skenario, hasil, dan kegagalan yang benar-benar ditemukan.
- [ ] Update status checklist utama hanya sesuai aturan dokumen utama; jangan menandai tahap yang belum diverifikasi.

**Lulus jika:** seluruh tes khusus template yang relevan lulus, tidak ada regresi yang diketahui, dan bukti pengujian tercatat.

## 6. Format Bukti Pengujian

Untuk setiap tahap yang akan dicentang, catat:
- **Tahap/item:** ID item checklist.
- **Lingkungan:** browser dan ukuran viewport jika pengujian browser dilakukan.
- **Langkah:** tindakan yang benar-benar dijalankan.
- **Hasil yang diharapkan:** sesuai acceptance criteria.
- **Hasil aktual:** apa yang benar-benar terjadi.
- **Status:** lulus/gagal/belum diuji.
- **Bukti:** screenshot, log, atau referensi perubahan bila tersedia.

Pembacaan source code saja tidak membuktikan interaksi runtime. Build yang berhasil tidak membuktikan kesetiaan visual. Screenshot yang cocok tidak membuktikan fungsi edit, undo/redo, atau export.

## 7. Aturan Mengelola Perubahan Checklist

- Checklist utama `silit_visual_editor_checklist.md` tetap tidak diubah kecuali status kotak centang yang memang diperbolehkan oleh aturan owner.
- Dokumen ini tidak boleh ditulis ulang atau ditambah requirement setelah disetujui; progres hanya diperbarui lewat status checkbox.
- Jangan mencentang beberapa tahap sekaligus hanya untuk menunjukkan progres.
- Jangan mencentang item jika ada bagian penting yang gagal atau belum diuji.
- Jika acceptance criteria ternyata tidak mungkin dipenuhi karena batas teknis, berhenti dan ajukan penjelasan serta opsi kepada owner sebelum mengubah scope.

## 8. Di Luar Scope

Yang berikut tetap ditunda dan tidak boleh dimulai berdasarkan dokumen ini:
- Supabase, Cloudflare R2, database, backend, atau persistence.
- Login, akun pengguna, atau sinkronisasi cloud.
- Template Isi/Langkah Memasak baru yang belum diberikan sumbernya.
- Template marketplace/import otomatis.
- Refactor umum di luar kebutuhan sistem template.
- Deployment.
- Perbaikan temuan teknis lain yang tidak menjadi prasyarat langsung.

## 9. Definition of Done Keseluruhan

Pekerjaan khusus ini baru boleh dinyatakan selesai jika:
- Semua tahap yang relevan telah diverifikasi.
- Classic tetap dapat diedit dan tidak mengalami regresi.
- Cover Double Smash dapat diedit per elemen utama.
- Template dapat memiliki komposisi elemen yang berbeda tanpa merusak editor bersama.
- Popup pemilihan template dan alur Add Page berfungsi.
- Urutan dan nomor halaman benar.
- Operasi halaman dan history tetap bekerja.
- A4 dan print/export lolos pengujian yang relevan.
- Tidak ada klaim pengujian yang dibuat tanpa bukti.
- Tidak ada deployment.
- Checklist utama tetap mematuhi urutan dan ketentuan aslinya.

**Aturan akhir:** dokumen ini mengatur urutan kerja khusus template, tetapi tidak mengesampingkan dokumen wajib SILIT. Jika ada konflik, ketidakjelasan, atau kebutuhan di luar scope, hentikan pekerjaan dan minta keputusan owner.
