# SILIT — Catatan Temuan Teknis Source Code

**Status:** Catatan temuan untuk ditinjau nanti  
**Repository kode:** `silit`  
**Repository dokumentasi:** `silitdoc`  
**Branch:** `main`  
**Tujuan:** Mencatat risiko dan kemungkinan defect yang ditemukan saat membaca source code. Dokumen ini bukan checklist kerja baru dan tidak mengubah urutan atau requirement pada `silit_visual_editor_checklist.md`.

---

## 1. Arahan Owner dan Batas Pengerjaan

Untuk fase saat ini, fokus pengerjaan adalah revisi UI/UX terlebih dahulu.

**Jangan menambahkan Supabase, Cloudflare R2, database, backend, atau layanan penyimpanan pada fase UI/UX ini.** Integrasi tersebut sengaja ditunda sampai owner menyatakan siap dan memberi instruksi yang jelas.

Alasan yang dicatat dari owner:
- Integrasi backend/storage terlalu dini membuat pengerjaan dan debugging lebih rumit.
- Perubahan UI/UX perlu distabilkan terlebih dahulu.
- Integrasi persistence perlu dikerjakan sebagai pekerjaan terpisah dengan scope, model data, dan verifikasi yang jelas.

Catatan ini bukan keputusan bahwa Supabase atau R2 pasti akan digunakan. Pilihan teknologi, rancangan data, dan strategi penyimpanan belum ditetapkan di dokumen ini.

### Aturan untuk AI yang melanjutkan pekerjaan

1. Jangan memperbaiki temuan di bawah secara otomatis hanya karena dokumen ini tersedia.
2. Lanjutkan revisi UI/UX sesuai checklist utama dan instruksi owner.
3. Jangan menambah atau mengubah requirement checklist utama melalui dokumen ini.
4. Jangan menambahkan Supabase, R2, backend, database, atau persistence sebelum ada instruksi/approval eksplisit dari owner.
5. Saat owner siap membahas temuan teknis, periksa ulang source code terbaru. Jangan menganggap line number, perilaku, atau temuan di bawah masih sama setelah perubahan kode.
6. Bedakan temuan dari pembacaan statis dengan defect yang sudah direproduksi di browser. Jangan menyebut temuan sebagai bug terverifikasi tanpa pengujian yang nyata.
7. Jika perbaikan membutuhkan perubahan di luar checklist utama, jelaskan masalah, alasan, dampak terhadap checklist, dan usulan scope; lalu tunggu approval.

---

## 2. Dasar Pemeriksaan dan Batas Verifikasi

Pemeriksaan sebelumnya membaca source code aplikasi, terutama:
- `recipe_generator_template_editor.tsx`
- `src/index.css`
- `src/main.tsx`
- `package.json`
- `vercel.json`
- konfigurasi Vite dan Tailwind.

Temuan di bawah merupakan **hasil pemeriksaan statis pada source code yang tersedia saat pemeriksaan**. Pemeriksaan tersebut tidak berhasil menjalankan build lokal karena lingkungan tidak dapat mengakses GitHub. Karena itu, temuan yang belum direproduksi di browser diberi status **perlu verifikasi**, bukan dianggap sudah terbukti saat runtime.

---

## 3. Daftar Temuan

### T-01 — Perubahan editor belum memiliki persistence

**Status:** Perlu direncanakan; tidak dikerjakan pada fase UI/UX.  
**Area:** Model data dan penyimpanan.

State editor diinisialisasi dari data awal di aplikasi. Pada source code yang diperiksa, tidak ditemukan integrasi penyimpanan melalui `localStorage`, `sessionStorage`, IndexedDB, API backend, Supabase, atau R2.

**Risiko yang perlu diuji nanti:** perubahan pengguna mungkin hanya berada di state aplikasi dan tidak bertahan setelah halaman dimuat ulang atau sesi berakhir.

**Catatan penting:** ini bukan izin untuk langsung menambahkan layanan penyimpanan. Sebelum implementasi, owner perlu menentukan kebutuhan penyimpanan, model data, perilaku pemulihan, dan teknologi yang disetujui.

**Referensi source:** [recipe_generator_template_editor.tsx](https://github.com/omegasands87/silit/blob/main/recipe_generator_template_editor.tsx) — inisialisasi data/state sekitar baris 198–218.

### T-02 — Perilaku shortcut paste belum tampak seperti membuat duplikat

**Status:** Perlu verifikasi perilaku dan ekspektasi produk.  
**Area:** Keyboard interaction.

Handler `Ctrl/Cmd+C` menyimpan elemen yang dipilih. Handler `Ctrl/Cmd+V` yang diperiksa tampak mengubah geometri/style elemen terpilih, bukan membuat elemen baru.

**Risiko:** pengguna dapat mengharapkan paste membuat salinan, tetapi perilakunya mungkin hanya mengubah elemen yang ada.

**Yang perlu dipastikan nanti:** apakah shortcut dimaksudkan untuk menduplikasi elemen, menyalin properti, atau memiliki perilaku lain. Jangan mengubah perilaku sebelum ekspektasinya dikonfirmasi.

**Referensi source:** [recipe_generator_template_editor.tsx](https://github.com/omegasands87/silit/blob/main/recipe_generator_template_editor.tsx) — sekitar baris 562–571.

### T-03 — Memilih elemen belum tentu membuka tab KONTEN

**Status:** Perlu verifikasi terhadap perilaku UI/UX yang diharapkan dan source terbaru.  
**Area:** Contextual inspector kanan.

Fungsi `selectElement` yang diperiksa memperbarui selection, tetapi tidak terlihat mengatur tab kanan ke `KONTEN`. Jika tab `DESAIN` sedang aktif, pemilihan elemen mungkin tidak otomatis berpindah ke `KONTEN`.

**Risiko:** konteks pengeditan yang ditampilkan bisa tidak sesuai dengan tindakan memilih elemen.

**Catatan:** dokumentasi pekerjaan sebelumnya menyebut pemilihan object secara default membuka KONTEN. Temuan ini perlu dibandingkan dengan source terbaru sebelum menyimpulkan ada regresi.

**Referensi source:** [recipe_generator_template_editor.tsx](https://github.com/omegasands87/silit/blob/main/recipe_generator_template_editor.tsx) — selection sekitar baris 277–289; tab inspector sekitar baris 687–705.

### T-04 — Risiko koordinat selection overlay pada halaman Langkah Memasak

**Status:** Risiko dari pembacaan statis; wajib direproduksi di browser.  
**Area:** Selection overlay dan pagination.

Selection overlay mencari elemen `.page-a4` pada preview aktif. Komponen halaman memasak juga membuat elemen pengukuran tersembunyi dengan class `.page-a4.cooking-pagination-measure` sebelum halaman yang terlihat. Fungsi pengukuran canvas memiliki pengecualian untuk elemen pengukuran tersebut, sedangkan pencarian pada overlay yang diperiksa tidak tampak memakai pengecualian yang sama.

**Risiko:** overlay selection dapat memakai koordinat halaman pengukuran tersembunyi, sehingga bounding box atau handle terlihat bergeser dari elemen yang dipilih.

**Verifikasi nanti:** pilih beberapa elemen pada halaman Langkah Memasak, termasuk langkah yang berpindah ke halaman lanjutan. Periksa posisi bounding box, handle resize, dan perilaku drag. Jangan menyatakan defect ini terkonfirmasi sebelum reproduksi.

**Referensi source:** [recipe_generator_template_editor.tsx](https://github.com/omegasands87/silit/blob/main/recipe_generator_template_editor.tsx) — overlay sekitar baris 1041–1045; measurement page dan pagination sekitar baris 1507–1534.

### T-05 — Multi-select mungkin sulit menghapus pilihan terakhir

**Status:** Perlu verifikasi interaksi.  
**Area:** Multi-selection.

Logika selection yang diperiksa menggunakan fallback ke elemen terpilih ketika daftar `multiSelected` kosong. Saat pengguna melakukan toggle untuk melepas elemen terakhir, fallback tersebut mungkin membuat elemen tetap dianggap terpilih.

**Risiko:** pengguna tidak dapat mengosongkan selection dengan cara yang mereka harapkan ketika memakai multi-select.

**Verifikasi nanti:** pilih satu elemen, gunakan modifier key untuk melepas pilihan itu, lalu periksa selected state, panel kanan, dan bounding box. Uji juga ketika ada lebih dari satu elemen terpilih.

**Referensi source:** [recipe_generator_template_editor.tsx](https://github.com/omegasands87/silit/blob/main/recipe_generator_template_editor.tsx) — logika selection sekitar baris 277–289.

### T-06 — Add Page dan Duplicate Page memiliki perilaku data yang berbeda

**Status:** Catatan arsitektur; belum tentu defect.  
**Area:** Manajemen halaman.

Source yang diperiksa menunjukkan Add Page membuat data berdasarkan default, sedangkan Duplicate Page menyalin data halaman aktif.

**Dampak:** kedua aksi memiliki perilaku berbeda terhadap isi halaman. Perbedaan ini bisa memang disengaja.

**Arahan:** pertahankan perilaku saat ini selama revisi UI/UX, kecuali checklist atau instruksi owner secara jelas meminta perubahan. Jika owner ingin mengubah perilakunya, sepakati ekspektasi terlebih dahulu.

**Referensi source:** [recipe_generator_template_editor.tsx](https://github.com/omegasands87/silit/blob/main/recipe_generator_template_editor.tsx) — pembuatan halaman sekitar baris 135–148 dan handler page sekitar baris 463–502.

### T-07 — Penomoran footer berpotensi tidak konsisten pada pagination

**Status:** Perlu verifikasi hasil canvas dan print.  
**Area:** Footer halaman Isi dan Langkah Memasak.

Pada source yang diperiksa, footer halaman Isi memakai teks nomor tetap `01`, sedangkan halaman Langkah Memasak menghitung nomor berdasarkan nomor halaman dan chunk pagination.

**Risiko:** penomoran bisa tidak konsisten ketika beberapa page type atau halaman hasil pagination digunakan bersama.

**Verifikasi nanti:** periksa penomoran di canvas dan hasil print untuk satu resep yang memiliki Cover, Isi, serta Langkah Memasak lebih dari satu halaman. Jangan mengubah nomor sebelum aturan penomoran yang diharapkan ditentukan.

**Referensi source:** [recipe_generator_template_editor.tsx](https://github.com/omegasands87/silit/blob/main/recipe_generator_template_editor.tsx) — footer halaman Isi sekitar baris 1386–1403; footer halaman memasak sekitar baris 1557–1573.

### T-08 — Layout responsive berisiko terpotong pada viewport kecil

**Status:** Risiko dari CSS statis; belum diuji di browser.  
**Area:** Responsive layout.

Shell editor memakai layout flex horizontal dengan sidebar kiri dan kanan yang memiliki ukuran dasar tetap. Media query pada ukuran kecil yang diperiksa mengubah ukuran sidebar kanan, tetapi tidak tampak mengubah susunan utama menjadi layout alternatif. Shell/body juga memakai overflow yang dapat membatasi area terlihat.

**Risiko:** pada viewport sempit, panel atau area editor bisa terpotong atau sulit dijangkau.

**Verifikasi nanti:** uji lebar desktop, tablet, dan mobile; periksa akses ke canvas, sidebar PAGE/LAYER, panel KONTEN/DESAIN, toolbar, serta scrolling. Jangan mengubah struktur sidebar yang sudah ditetapkan tanpa approval.

**Referensi source:** [src/index.css](https://github.com/omegasands87/silit/blob/main/src/index.css) — shell/sidebar sekitar baris 32–59; media query akhir sekitar baris 2084–2103.

### T-09 — Export saat ini menggunakan dialog print browser

**Status:** Catatan perilaku saat ini.  
**Area:** Print/export.

Source yang diperiksa menggunakan `window.print()` dan aturan CSS print. Tidak ditemukan library PDF khusus pada file dan konfigurasi yang diperiksa.

**Dampak:** hasil akhir bergantung pada perilaku print browser, pengaturan print, dan CSS print. Ini perlu dibedakan dari proses menghasilkan file PDF yang sepenuhnya dikendalikan aplikasi.

**Verifikasi nanti:** bandingkan tampilan canvas dengan print preview/PDF, termasuk ukuran A4, crop image, urutan layer, pagination, margin, dan footer. Jangan mengganti pendekatan export tanpa kebutuhan dan approval yang jelas.

**Referensi source:** [recipe_generator_template_editor.tsx](https://github.com/omegasands87/silit/blob/main/recipe_generator_template_editor.tsx) — handler print/export sekitar baris 558–575; aturan print berada di [src/index.css](https://github.com/omegasands87/silit/blob/main/src/index.css).

### T-10 — Pro Tip berpotensi overflow pada kasus langkah terakhir yang sangat tinggi

**Status:** Edge case yang perlu direproduksi.  
**Area:** Pagination Langkah Memasak.

Logika pagination yang diperiksa memindahkan langkah dari chunk terakhir selama chunk itu masih memiliki lebih dari satu langkah. Jika satu langkah terakhir sendiri ditambah Pro Tip melebihi ruang yang tersedia, ada kemungkinan konten tetap melebihi tinggi halaman.

**Verifikasi nanti:** uji deskripsi langkah terakhir yang sangat panjang, ditambah Pro Tip yang panjang. Periksa overflow pada canvas dan print/PDF. Jangan mengubah aturan pagination sebelum kasusnya direproduksi dan hasil yang diharapkan ditentukan.

**Referensi source:** [recipe_generator_template_editor.tsx](https://github.com/omegasands87/silit/blob/main/recipe_generator_template_editor.tsx) — logika pagination pada komponen CookingPage sekitar baris 1507–1534.

---

## 4. Catatan Struktur Proyek

- Source editor utama berada pada satu file React besar: `recipe_generator_template_editor.tsx`.
- Style utama berada pada `src/index.css`.
- `package.json` yang diperiksa memiliki script `dev`, `build`, dan `preview`, tetapi tidak memiliki script test.
- Tidak ditemukan test suite otomatis pada file yang diperiksa.
- Pemeriksaan source tidak membuktikan bahwa semua interaksi berjalan benar di browser.

Informasi ini adalah catatan keadaan source saat pemeriksaan, bukan larangan untuk merapikan arsitektur di masa depan. Refactor harus mengikuti scope yang disetujui owner.

---

## 5. Cara Menggunakan Dokumen Ini Nanti

Saat owner menyatakan siap membahas temuan teknis:

1. Baca ulang dokumen wajib dan checklist utama.
2. Periksa source terbaru di `silit/main`.
3. Reproduksi dan verifikasi temuan di browser sebelum mengubah kode.
4. Tentukan temuan mana yang benar-benar perlu diperbaiki dan urutan yang disetujui owner.
5. Untuk persistence, bahas kebutuhan dan pilihan teknologi secara terpisah. Jangan menganggap Supabase atau R2 sudah diputuskan.
6. Minta approval sebelum pekerjaan yang berada di luar checklist utama.
7. Catat hasil pengujian yang benar-benar dilakukan. Jangan mencentang checklist utama hanya berdasarkan catatan ini.

**Dokumen ini tidak mengizinkan implementasi otomatis. Prioritas saat ini tetap revisi UI/UX.**
