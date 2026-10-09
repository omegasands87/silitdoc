# SILIT — Spesifikasi Terkunci Perbaikan Editor Cover Double Smash

**Status:** BASELINE TERKUNCI — jangan ubah dokumen ini sampai seluruh perbaikan selesai.  
**Tanggal baseline:** 10 Oktober 2026  
**Repositori aplikasi:** `omegasands87/silit` — branch `main`  
**Repositori dokumentasi:** `omegasands87/silitdoc` — branch `main`  
**Template target:** `double-smash-cheeseburger`  
**Dokumen ini dibuat atas instruksi eksplisit user dan menjadi acuan kerja aktif untuk perbaikan ini.**

---

## 0. Aturan penguncian

1. Dokumen ini adalah kontrak kerja tetap untuk pekerjaan aktif ini.
2. Setelah dokumen dibuat, jangan mengubah, mengurangi, menambah, menulis ulang, atau menafsirkan ulang scope, urutan kerja, requirement, maupun acceptance criteria sampai seluruh perbaikan selesai.
3. Jangan mengubah dokumen ini untuk menyesuaikan implementasi yang gagal atau supaya checklist terlihat lulus.
4. Status yang belum diuji harus tetap dianggap belum terverifikasi. Membaca source, membuat commit, atau melihat satu screenshot tidak membuktikan semua interaksi berfungsi.
5. Jika implementasi menemukan masalah yang sudah termasuk substansi requirement dokumen ini, perbaiki tanpa meminta persetujuan ulang.
6. Jika ada kebutuhan baru yang benar-benar berada di luar scope dan tidak diperlukan untuk memenuhi requirement di sini, hentikan bagian tersebut dan minta instruksi user. Jangan memperluas pekerjaan sendiri.
7. Semua perubahan kode dilakukan langsung di branch `main` pada repo `silit`. Jangan membuat branch baru.
8. Perubahan dokumentasi/checklist berada di repo `silitdoc`. Dokumen ini tidak boleh diedit sampai perbaikan selesai. Catatan pelaksanaan dan bukti akhir boleh disusun setelah pekerjaan selesai; jangan mengubah acceptance criteria.
9. AI tidak boleh melakukan deployment, preview deployment, staging, redeploy, atau tindakan deployment lainnya. Deployment dan verifikasi URL produksi adalah tanggung jawab owner.
10. Jangan membuat backend, database, storage, atau layanan baru.
11. Jangan melakukan redesign artistik terhadap tampilan Double Smash. Pertahankan komposisi visual, aset gambar embedded, font embedded, warna, dan karakter desain asli kecuali perubahan teknis minimal terbukti diperlukan untuk memenuhi requirement.
12. Jangan merusak atau mengubah perilaku Cover Classic, Isi, Langkah Memasak, sidebar global, atau fitur editor lain. Shared component boleh disentuh hanya bila memang diperlukan untuk integrasi ini dan harus diuji regresinya.

## 1. Tujuan pekerjaan

Membuat cover Double Smash menjadi template yang dapat diedit secara wajar, konsisten, dan dapat diprediksi seperti tiga halaman editor sebelumnya: Cover Classic, Isi, dan Langkah Memasak.

Pengguna harus dapat mengetahui elemen apa yang bisa diedit, memilihnya dari canvas atau Layer, mengubah properti yang sesuai melalui panel KONTEN dan DESAIN, melihat perubahan diterapkan pada elemen yang benar, dan memulihkan perubahan dengan Undo/Redo.

Targetnya bukan sekadar membuat semua kontrol terlihat. Setiap kontrol yang tersedia harus bekerja, terhubung ke state yang benar, bertahan setelah pergantian selection/render, dan tidak merusak layout template.

## 2. Ruang lingkup tetap

### Termasuk

- Audit kontrak elemen dan kecocokannya dengan HTML template.
- Audit konten, selector DOM, geometri, hitbox, serta koordinat iframe/canvas.
- Sinkronisasi canvas, selection, daftar Layer, bounding box, dan panel kanan.
- Panel KONTEN untuk teks dan gambar.
- Panel DESAIN untuk teks, gambar, shape, dan dekorasi sesuai tipe.
- Drag, resize, rotasi, alignment, z-order, zoom, dan perubahan geometri yang didukung editor.
- Reset properti ke nilai asli template.
- Sinkronisasi state, rendering, Undo/Redo, pergantian halaman, dan duplikasi halaman.
- Export Current, Export All, print/PDF, serta regresi tiga page type lainnya.
- Build, automated/static checks, dan browser tests yang tersedia.
- Verifikasi terhadap desain dan aset asli.

### Tidak termasuk

- Redesign artistik atau penggantian konsep desain Double Smash.
- Penambahan fitur baru yang tidak diperlukan untuk ketereditan yang diminta.
- Backend, database, storage, atau layanan baru.
- Perubahan template resep lain yang tidak diperlukan.
- Perubahan struktur sidebar global `PAGE`/`LAYER` di kiri dan `KONTEN`/`DESAIN` di kanan.
- Deployment oleh AI.

## 3. Kondisi awal dan cara membaca bukti

Dokumentasi sebelumnya memuat beberapa snapshot audit dan log yang dibuat pada tahap berbeda. Angka kontrak pada snapshot lama tidak boleh dianggap otomatis menggambarkan source saat pengerjaan dimulai. Sebelum mengubah kode, periksa ulang source terbaru pada branch `main`.

Log terdahulu mencatat kontrak 28 elemen (19 teks, 1 gambar, 8 shape) dan pemeriksaan statis terhadap selector/ID. Itu adalah petunjuk audit, bukan pengganti pemeriksaan ulang pada source terkini maupun browser test. Jangan menganggap seluruh elemen sudah berfungsi hanya karena terdaftar di kontrak.

Arsitektur yang perlu ditelusuri dan diverifikasi pada source terbaru:

1. Template HTML Double Smash dimuat melalui iframe.
2. Lapisan interaksi editor membuat hitbox di atas iframe dari geometri node DOM.
3. Kontrak elemen menghubungkan ID, tipe, label, selector/geometri, dan content key.
4. Panel KONTEN membaca definisi kontrak dan mengubah data konten/gambar.
5. Panel DESAIN mengubah style serta properti geometri.
6. State model halaman dan DOM template harus tetap sinkron setelah setiap interaksi.

Jika source aktual berbeda dari uraian ini, ikuti source yang terverifikasi dan catat perbedaannya pada catatan kerja; jangan mengarang perilaku yang belum diperiksa.

## 4. Requirement dan acceptance criteria

Semua kelompok di bawah wajib lulus. Satu kelompok belum lulus jika ada elemen atau alur penting yang gagal.

### A. Inventaris elemen dan kontrak

- [ ] Audit seluruh elemen visual yang benar-benar ada pada HTML template.
- [ ] Cocokkan setiap elemen dengan ID unik, tipe, label Layer, selector sumber, geometri, dan content key bila relevan.
- [ ] Pastikan tidak ada elemen visual yang seharusnya dapat diedit tetapi tidak terdaftar.
- [ ] Pastikan tidak ada item Layer palsu, duplikat, atau tidak memiliki target DOM yang valid.
- [ ] Pastikan setiap selector unik dan menunjuk node yang benar pada runtime, termasuk elemen yang dibuat dinamis bila masih ada.
- [ ] Pisahkan elemen teks, gambar, shape, dan dekorasi berdasarkan perilaku yang memang diperlukan.
- [ ] Elemen background/shade yang menutupi area besar tidak boleh merebut klik canvas dari elemen lain. Jika dipilih melalui Layer, perilakunya harus jelas dan berfungsi.
- [ ] Buat pemeriksaan otomatis/static guard untuk kontrak jika memungkinkan dalam struktur proyek yang ada.

**Lulus jika:** inventaris kontrak cocok dengan HTML aktual; tidak ada target yang hilang, salah, ambigu, atau tidak dapat diidentifikasi.

### B. Selection, Layer, dan hitbox

- [ ] Klik setiap elemen yang memang dapat dipilih pada canvas memilih ID yang benar.
- [ ] Memilih elemen dari Layer memilih target canvas yang sama.
- [ ] Highlight, bounding box, label, dan panel kanan selalu mengacu pada ID yang sama.
- [ ] Elemen yang berdekatan atau bertumpuk tidak membuat selection salah sasaran.
- [ ] Hitbox mengukur node visual yang tepat, bukan parent yang ikut mencakup teks/dekorasi lain kecuali perilaku grup memang disengaja.
- [ ] Perubahan teks, font, ukuran, lebar, gambar, dan layout memicu pengukuran ulang hitbox.
- [ ] Koordinat iframe-to-canvas konsisten dan tidak bergeser.
- [ ] Uji zoom 50%, 75%, 100%, Fit, perubahan ukuran viewport, dan perubahan lebar sidebar.
- [ ] Klik area kosong mengikuti perilaku editor yang sudah berlaku dan tidak menyebabkan canvas blank.
- [ ] Elemen dekoratif yang tidak bisa dipilih lewat canvas tetap dapat diakses melalui Layer jika memang editable.
- [ ] Selection tidak berpindah sendiri setelah state update, pergantian tab, atau render ulang.

**Lulus jika:** selection dari canvas dan Layer konsisten; hitbox tepat pada semua skenario uji; tidak ada salah pilih atau drift yang teramati.

### C. Panel KONTEN

- [ ] Semua teks yang ditujukan untuk pengguna memiliki field konten yang benar.
- [ ] Mengubah field hanya mengubah target yang sesuai; sibling markup dan penekanan teks tidak rusak.
- [ ] Teks pendek, panjang, kosong, multibaris, dan karakter Bahasa Indonesia ditangani dengan benar.
- [ ] Elemen teks yang memiliki penekanan berbeda dapat diedit secara terpisah sesuai kontrak.
- [ ] Jika parent dan child memiliki teks berbeda, mengedit salah satunya tidak menghapus atau mengubah yang lain.
- [ ] Gambar burger dapat diganti lewat upload dan URL.
- [ ] Tombol gambar bawaan memulihkan aset embedded asli, bukan URL atau upload sebelumnya.
- [ ] Menghapus URL mengikuti perilaku fallback yang benar dan tidak menampilkan gambar lama yang tidak sesuai.
- [ ] Panel saat satu Layer dipilih menampilkan field yang sesuai; mode semua konten tetap masuk akal ketika tidak ada elemen terpilih.
- [ ] Shape/dekorasi tidak diberi field teks palsu; panel menjelaskan bahwa pengaturannya ada di DESAIN.
- [ ] Perubahan konten tetap ada setelah pemilihan ulang, pindah tab, pindah halaman, dan Undo/Redo.

**Lulus jika:** setiap field mengubah data dan target yang benar; gambar dapat diganti dan dipulihkan; tidak ada markup atau konten tetangga yang rusak.

### D. Panel DESAIN

Panel harus konsisten secara pola dengan tiga halaman sebelumnya, tetapi kontrol harus sesuai dengan tipe elemen. Jangan menampilkan kontrol yang tidak relevan hanya demi menyamakan jumlah kontrol.

- [ ] Teks memiliki kontrol yang relevan dan berfungsi untuk font, ukuran, weight, italic, uppercase bila tersedia, line-height, letter-spacing, alignment, warna teks, background bila didukung, posisi, ukuran, rotasi, opacity, border/radius/shadow bila relevan, dan reset.
- [ ] Gambar memiliki kontrol yang relevan dan berfungsi untuk ukuran/frame, fit/crop, zoom, offset/posisi gambar, opacity, geometri yang didukung, dan reset.
- [ ] Shape/dekorasi memiliki kontrol visual yang relevan: warna, opacity, posisi/ukuran/rotasi jika diizinkan, border/radius/shadow bila relevan, dan reset.
- [ ] Background atau elemen dasar yang berisiko merusak seluruh komposisi boleh membatasi transformasi jika ada alasan teknis; pembatasan harus konsisten dan tidak membuat kontrol palsu.
- [ ] Semua kontrol warna yang ditampilkan menyediakan input HEX yang konsisten jika kontrol warna lain di editor sudah mendukungnya.
- [ ] Default font, warna, gradient, crop, dan properti desain berasal dari template asli, bukan nilai perkiraan.
- [ ] Reset menghapus override editor dan mengembalikan gaya asli template.
- [ ] Setiap kontrol benar-benar diterapkan ke node/ID yang dipilih, bukan hanya mengubah nilai input.
- [ ] Nilai yang terlihat di panel tetap cocok dengan hasil canvas setelah selection diganti dan dipilih kembali.
- [ ] Mengubah style satu elemen tidak mengubah elemen lain secara tidak sengaja melalui CSS inheritance.
- [ ] Nilai kosong/auto ditangani secara konsisten dan dapat dipulihkan.

**Lulus jika:** kontrol yang terlihat semuanya bekerja, relevan dengan tipe elemen, tidak memengaruhi elemen lain secara tak sengaja, dan nilai panel/canvas sinkron.

### E. Transformasi dan urutan layer

- [ ] Drag mengubah posisi elemen yang benar.
- [ ] Resize mengubah dimensi yang benar dan tidak menggeser elemen lain.
- [ ] Rotasi bekerja bila didukung untuk tipe elemen tersebut.
- [ ] Alignment mengacu pada koordinat canvas yang benar.
- [ ] Pengaturan X/Y/width/height pada panel sinkron dengan drag/resize.
- [ ] Z-order/naik/turun/ke depan/ke belakang menghasilkan urutan visual yang sesuai dengan Layer, dengan memperhitungkan stacking context CSS template.
- [ ] Elemen terkunci atau yang transformasinya memang dilarang tidak menampilkan affordance yang menyesatkan.
- [ ] Transformasi tidak merusak ukuran halaman A4, rasio artwork, footer, atau posisi elemen lain.
- [ ] Transformasi tetap benar pada zoom 50%, 75%, 100%, dan Fit.

**Lulus jika:** perubahan geometri/urutan sesuai dengan tindakan pengguna dan tidak menghasilkan drift atau kerusakan layout.

### F. State, Undo/Redo, dan siklus halaman

- [ ] Perubahan konten, style, gambar, posisi, ukuran, rotasi, dan urutan layer dapat dipulihkan dengan Undo/Redo sesuai kemampuan editor.
- [ ] Undo/Redo tidak membuat state panel berbeda dari canvas.
- [ ] Pindah ke halaman lain lalu kembali tidak menghilangkan atau menerapkan perubahan pada halaman yang salah.
- [ ] Duplicate Page tidak membuat halaman baru berbagi state mutable dengan sumbernya secara tidak sengaja.
- [ ] Lifecycle iframe, font loading, dan pengukuran ulang tidak membuat perubahan kembali ke default atau hitbox usang.
- [ ] Tidak ada update state yang mengakibatkan selection salah, perubahan ganda, atau hilangnya elemen.
- [ ] Fitur dan data yang sudah ada di halaman lain tetap utuh.

**Lulus jika:** perubahan dapat diprediksi sepanjang siklus edit, Undo/Redo, pemilihan ulang, pindah halaman, dan duplikasi.

### G. Export, print, build, dan regresi

- [ ] `npm run build` selesai tanpa error.
- [ ] Automated/static verification yang tersedia berjalan dan hasilnya dicatat.
- [ ] Browser test dilakukan pada seluruh elemen kontrak dan kontrol utama.
- [ ] Export Current menghasilkan cover yang sesuai dengan canvas.
- [ ] Export All/print mempertahankan desain, font, gambar, warna, ukuran A4, dan layout.
- [ ] Tidak ada hitbox, selection outline, panel, atau kontrol editor yang ikut masuk ke hasil ekspor.
- [ ] Uji regresi Cover Classic, Isi, dan Langkah Memasak: rendering, selection, panel KONTEN/DESAIN, transformasi yang sudah ada, pergantian halaman, dan export tetap berfungsi.
- [ ] Setiap kegagalan dicatat dan diperbaiki sebelum kelompok ini dinyatakan lulus.
- [ ] Tidak ada klaim lulus untuk browser/export jika lingkungan uji tidak tersedia; tandai sebagai belum terverifikasi dan jelaskan batasannya.

**Lulus jika:** build dan pemeriksaan yang tersedia sukses; browser dan export lolos; regresi pada tiga page type lainnya tidak ditemukan.

## 5. Alur kerja wajib

Urutan ini tidak boleh dilompati. Jangan mulai coding sebelum audit source dan inventaris awal selesai.

### Tahap 1 — Kunci baseline source

1. Baca aturan wajib dan checklist yang terkait di repo `silitdoc`.
2. Periksa branch `main` dan source terbaru di repo `silit`.
3. Catat SHA file relevan sebelum perubahan: editor utama, HTML template, CSS, package scripts, dan test/verifier.
4. Jalankan atau periksa automated/static verifier yang sudah ada jika lingkungan memungkinkan.
5. Jangan menganggap angka/temuan dari snapshot lama masih sama tanpa memeriksa source terkini.

**Gate 1:** baseline source dan cara menjalankan build/test diketahui.

### Tahap 2 — Audit end-to-end tanpa mengubah kode

1. Inventaris seluruh elemen visual aktual.
2. Telusuri alur setiap elemen: kontrak → state/data → selector DOM → geometri/hitbox → selection/Layer → panel KONTEN/DESAIN → export.
3. Catat kontrol yang ada, kontrol yang hilang, kontrol yang tidak relevan, dan kontrol yang tampak ada tetapi tidak bekerja.
4. Bedakan dengan tegas temuan source yang terkonfirmasi dari perilaku yang belum diuji di browser.
5. Bandingkan pola interaksi dengan Cover Classic, Isi, dan Langkah Memasak tanpa mengubah struktur sidebar global.
6. Prioritaskan akar masalah; jangan menutup gejala dengan z-index, offset perkiraan, atau penambahan kontrol tanpa hubungan state yang benar.

**Gate 2:** setiap requirement memiliki pemahaman implementasi dan metode verifikasi yang jelas.

### Tahap 3 — Perbaikan kontrak, DOM, dan geometri

1. Pastikan kontrak memetakan semua target aktual secara unik.
2. Perbaiki selector parent/child yang tumpang tindih dan target yang bukan node edit yang tepat.
3. Pastikan content update mempertahankan markup sibling yang diperlukan.
4. Pastikan pengukuran hitbox berasal dari geometri node yang tepat.
5. Pastikan konversi koordinat iframe/canvas tunggal dan konsisten.
6. Pastikan pengukuran ulang terjadi setelah perubahan konten, style, font, gambar, dan ukuran viewport.
7. Tambahkan atau perkuat guard agar kontrak yang tidak valid tidak gagal secara diam-diam.

**Gate 3:** pemeriksaan statis/otomatis untuk kontrak dan pemetaan lolos sebelum melanjutkan ke panel.

### Tahap 4 — Perbaikan selection dan Layer

1. Uji klik canvas dan klik Layer untuk setiap tipe elemen.
2. Sinkronkan selection ID, highlight, bounding box, dan panel kanan.
3. Selesaikan konflik hitbox tanpa membuat dekorasi besar menangkap klik.
4. Uji zoom, viewport, resize sidebar, dan perubahan teks.
5. Periksa drag, resize, rotasi, alignment, dan z-order sesuai tipe elemen.

**Gate 4:** selection dan transformasi utama stabil di browser.

### Tahap 5 — Perbaikan panel KONTEN dan DESAIN

1. Pastikan field KONTEN sesuai dengan content key setiap elemen.
2. Uji teks pendek/panjang/kosong/multibaris dan pemisahan emphasis.
3. Uji upload, URL, fallback, dan pemulihan gambar embedded.
4. Cocokkan kontrol DESAIN dengan tipe elemen.
5. Telusuri setiap kontrol dari input → state → DOM/style → canvas; jangan menyatakan selesai hanya karena nilai input berubah.
6. Pastikan font/warna/crop/default berasal dari template asli dan reset mengembalikannya.
7. Uji isolation: properti satu elemen tidak boleh bocor ke sibling.

**Gate 5:** semua kontrol konten dan desain yang disyaratkan berfungsi serta konsisten.

### Tahap 6 — State dan alur lintas halaman

1. Uji Undo/Redo untuk konten, gambar, style, geometri, dan urutan layer.
2. Uji pindah tab dan pemilihan ulang.
3. Uji pindah halaman, kembali, dan Duplicate Page.
4. Periksa lifecycle iframe/font serta sinkronisasi state dan DOM.
5. Perbaiki hanya masalah yang berada dalam scope dokumen ini.

**Gate 6:** siklus editing tidak kehilangan perubahan dan tidak mengubah halaman yang salah.

### Tahap 7 — Verifikasi akhir

1. Jalankan automated/static checks.
2. Jalankan `npm run build`.
3. Jalankan browser tests untuk semua elemen dan interaksi yang diwajibkan.
4. Uji Export Current dan Export All/print.
5. Jalankan regresi Cover Classic, Isi, dan Langkah Memasak.
6. Perbaiki semua kegagalan yang termasuk scope, lalu ulangi tes terkait.
7. Catat hasil dengan bukti nyata, termasuk tes yang tidak dapat dijalankan dan alasannya.
8. Jangan deploy. Serahkan hasil dan commit SHA kepada owner untuk deployment mandiri.

**Gate 7 / selesai:** seluruh acceptance criteria lulus dan bukti verifikasi tersedia, atau secara eksplisit dicatat bahwa pekerjaan belum selesai karena ada tes yang belum dapat dijalankan. Tidak boleh menyatakan selesai jika ada kriteria wajib yang belum terverifikasi.

## 6. Format bukti yang diperlukan

Untuk setiap kelompok acceptance criteria, bukti akhir harus menyebutkan:

- Item/kelompok yang diperiksa.
- Metode: source inspection, automated check, build, atau browser test.
- Hasil aktual: PASS, FAIL, atau NOT VERIFIED.
- Bukti yang dapat diperiksa: command dan output ringkas, hasil test, langkah reproduksi, screenshot/video bila relevan, serta commit SHA terkait.
- Jika gagal: perilaku aktual, perilaku yang diharapkan, akar masalah yang ditemukan, dan status perbaikannya.
- Jika tidak bisa diuji: hambatan yang spesifik. Jangan menggantinya dengan klaim dari source atau screenshot.

## 7. Definisi selesai

Pekerjaan baru boleh dinyatakan selesai jika:

1. Semua elemen yang dimaksudkan untuk diedit dapat ditemukan dan diedit melalui alur yang tepat.
2. Selection canvas, Layer, bounding box, dan panel kanan konsisten.
3. Panel KONTEN dan DESAIN lengkap menurut tipe elemen dan seluruh kontrol yang terlihat benar-benar berfungsi.
4. Perubahan tidak merusak struktur, desain asli, aset, atau sibling elements.
5. Geometri, zoom, Undo/Redo, pergantian halaman, duplikasi, dan export lolos pengujian yang ditetapkan.
6. Build, automated checks, browser tests, dan regresi yang diwajibkan telah dijalankan; setiap batasan tes dilaporkan secara jujur.
7. Cover Classic, Isi, dan Langkah Memasak tidak mengalami regresi.
8. Tidak ada deployment yang dilakukan oleh AI.

Dokumen ini tetap menjadi baseline tetap sampai semua perbaikan selesai. Requirement tidak boleh diubah hanya karena implementasi sulit atau tes belum tersedia.
