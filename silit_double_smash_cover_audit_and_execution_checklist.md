# SILIT — Audit dan Checklist Eksekusi Cover Double Smash

**Status dokumen:** BASELINE TERKUNCI  
**Target implementasi:** `silit` branch `main`  
**Lokasi dokumentasi:** `silitdoc` branch `main`  
**Scope:** hanya cover template `double-smash-cheeseburger` beserta integrasi editornya.  
**Deployment:** hanya owner yang boleh melakukan deploy. AI tidak boleh melakukan deploy, preview deployment, staging, atau redeploy.

## 0. Aturan baseline

1. Dokumen ini adalah spesifikasi kerja tetap untuk audit dan perbaikan cover Double Smash.
2. Setelah baseline ini dibuat, requirement, urutan, scope, dan kriteria lulus tidak boleh diubah sepihak. Checkbox boleh diperbarui hanya untuk mencatat status nyata; wording dan urutan item tidak boleh diubah.
3. Pekerjaan harus dilakukan mengikuti checklist dari atas ke bawah. Jangan melewati item.
4. AI mengerjakan seluruh pekerjaan kode, dokumentasi bukti, build, automated test, dan browser test yang dapat dijalankan secara mandiri. Hanya deployment dan verifikasi pascadeploy di URL produksi yang menjadi tugas owner.
5. Jangan menyatakan item lulus hanya berdasarkan commit, pembacaan source, atau screenshot. Setiap item harus memiliki bukti yang sesuai dengan metode verifikasinya.
6. Jangan mengubah template Classic, halaman Isi, Langkah Memasak, struktur sidebar global, atau fitur di luar integrasi Double Smash kecuali perubahan teknis minimal terbukti diperlukan untuk memperbaiki integrasi ini. Jika perubahan lintas halaman diperlukan, pastikan tidak ada perubahan perilaku halaman lain dan uji regresi.
7. Pertahankan desain visual asli Double Smash sebagai baseline. Perbaiki ketereditan, ketepatan hitbox, dan kestabilan layout; jangan melakukan redesign artistik tanpa instruksi.
8. Jangan deploy. Perubahan kode dilakukan langsung di branch `main` sesuai aturan repo SILIT.

## 1. Bukti audit source

Audit statis dilakukan pada:
- `silit/recipe_generator_template_editor.tsx`
- `silit/src/index.css`
- `silit/public/templates/cover-double-smash-cheeseburger.html`
- `silit/package.json`
- `silitdoc/silit_ai_mandatory_rules.md`
- `silitdoc/silit_visual_editor_checklist.md`

### 1.1 Model elemen

Kontrak template Double Smash saat audit memiliki **28 elemen**:
- **19 teks** yang mempunyai `contentKey` dan harus dapat diedit dari panel Konten serta panel Desain.
- **1 gambar** burger yang harus dapat diganti dari panel Konten dan diatur dari panel Desain.
- **8 shape/dekorasi** yang tidak memiliki teks dan hanya memerlukan kontrol visual.

Selector kontrak diperiksa terhadap HTML template saat audit: **28 dari 28 selector ditemukan tepat satu kali**. Untuk semua definisi saat ini, `geometryRef` sama dengan `sourceSelector`. Ini adalah hasil pemeriksaan statis, bukan bukti bahwa hitbox selalu tepat pada setiap ukuran viewport atau setelah perubahan style.

### 1.2 Temuan yang terkonfirmasi dari source

**F-01 — Kegagalan selector tidak terlihat di UI produksi.**  
`HTMLCoverPage` melewati definisi jika model elemen, source node, atau geometry node tidak ditemukan. Peringatan hanya ditulis melalui `console.warn` saat `import.meta.env.DEV`. Pada produksi, elemen yang hilang bisa menghilang dari hitbox tanpa pesan yang terlihat bagi pengguna. Perbaikan harus menyediakan validasi kontrak dan jalur error yang eksplisit, bukan diam-diam menghilangkan elemen.

**F-02 — Background dan shade tidak dapat dipilih langsung melalui canvas.**  
Hitbox untuk `cover-background` dan `cover-shade` diberi `pointer-events: none`. Keduanya masih tersedia di Layer. Perilaku ini mencegah elemen yang menutupi area besar memblokir target lain, tetapi pengguna perlu mengetahui bahwa kedua elemen dipilih melalui Layer. Background/shade tidak boleh dibuat menangkap seluruh klik canvas.

**F-03 — Teks deskripsi terdiri dari node yang berdekatan dan memiliki aturan CSS berbeda.**  
Bagian deskripsi waktu menggunakan `.silit-time-label`, `.silit-time-emphasis`, `.silit-feature-line`, `.silit-feature-prefix`, dan `.silit-feature-emphasis` di dalam `.cover-time-story`. Sebagian aturan berasal dari selector induk seperti `.cover-time-story > span` dan `.cover-time-story strong`, bukan class individual. Mengganti font, ukuran, line-height, lebar, atau isi dapat mengubah wrapping dan dimensi hitbox. Ini harus diuji dengan teks pendek/panjang dan kombinasi tipografi, bukan diperbaiki dengan mengira-ngira koordinat.

**F-04 — Model visual menggunakan dua lapis koordinat.**  
HTML asli diskalakan oleh `fitCover()` pada template. Editor mengukur node melalui `getBoundingClientRect()`, mengonversi koordinat frame ke canvas A4, lalu menggambar hitbox terpisah di atas iframe. Drag/resize menyimpan posisi/ukuran model dan renderer mengaplikasikannya ke node HTML. Perubahan pada perhitungan skala atau pengukuran harus mempertahankan satu konversi koordinat yang konsisten.

**F-05 — Update konten memodifikasi DOM template.**  
`applyDoubleSmashContent` menulis melalui `node.textContent`. Semua target teks pada kontrak saat audit adalah target leaf teks, jadi ini mencegah sibling markup terhapus. Syarat ini harus dipertahankan: jangan arahkan `contentKey` ke parent yang berisi elemen anak seperti judul gabungan atau seluruh paragraf.

**F-06 — Style disimpan pada model elemen dan `page.elementStyles`.**  
`updateElementStyle` memperbarui keduanya untuk Double Smash; renderer menerapkan sebagian properti dari `element.style`, `x/y`, `width/height`, `rotation`, dan data gambar. Setiap properti kontrol harus terbukti mencapai node target dan bertahan setelah pemilihan elemen, perpindahan halaman, undo/redo, serta export.

**F-07 — Kontrol gambar memiliki dua sumber perubahan.**  
Panel Konten mengganti gambar melalui upload atau URL `page.data.burgerImage`; panel Desain mengubah crop/fit, zoom, offset, opacity, dan geometri frame. Keduanya harus tetap sinkron. Tombol `Foto Bawaan` harus mengembalikan aset embedded asli, bukan URL atau data dari upload sebelumnya.

**F-08 — Desain template memiliki font dan CSS embedded.**  
Template menyertakan font dan aset embedded serta aturan tipografi spesifik. Nilai default harus berasal dari template asli. Reset style harus menghapus override editor sehingga CSS asli kembali berlaku; jangan mengganti default desain dengan nilai perkiraan.

**F-09 — Ada perbedaan antara definisi statis dan perilaku runtime.**  
Pemeriksaan statis mengonfirmasi 28 selector unik, tetapi tidak menguji hasil bounding box, event pointer, font yang sudah selesai dimuat, resize, export, atau state undo/redo di browser. Semua itu harus diuji sebelum dinyatakan lulus.

### 1.3 Hal yang belum boleh dianggap sebagai temuan terkonfirmasi

- Akar penyebab akhir teks bertumpuk pada setiap kondisi belum dibuktikan hanya dengan membaca source.
- Belum ada hasil build/browser test untuk baseline audit ini.
- Tidak ada klaim bahwa semua 28 hitbox sudah akurat secara visual hanya karena semua selector ditemukan.
- Tidak ada klaim bahwa export HTML/PDF identik dengan canvas sebelum pengujian langsung.

## 2. Target perilaku final

### 2.1 Sinkronisasi elemen

Untuk setiap definisi elemen:
- ID kontrak unik dan konsisten dengan model element.
- Label Layer manusiawi dan tidak jatuh ke ID teknis jika label yang relevan seharusnya tersedia.
- Selector sumber ditemukan tepat satu kali.
- Selector geometri ditemukan tepat satu kali dan mengukur objek yang sama dengan target yang diedit, kecuali pengecualian dijelaskan eksplisit.
- Tipe `text`, `image`, dan `shape` sesuai dengan struktur HTML.
- Field Konten dan kontrol Desain sesuai tipe elemen.
- Tidak ada elemen visual yang tidak dapat dijangkau dari canvas maupun Layer.

### 2.2 Editing teks

Elemen teks mandiri:
1. Kategori.
2. Judul baris pertama.
3. Judul baris kedua.
4. Deskripsi intro baris pertama.
5. Awalan intro baris kedua.
6. Penekanan protein.
7. Label waktu.
8. Durasi.
9. Deskripsi waktu baris pertama.
10. Awalan deskripsi baris kedua.
11. Penekanan deskripsi baris kedua.
12. Label dan nilai Persiapan.
13. Label dan nilai Memasak.
14. Label dan nilai Kalori.
15. Label dan nilai Porsi.

Kriteria:
- Setiap teks bisa dipilih secara mandiri di canvas jika hitbox tidak sengaja ditutup elemen lain, dan selalu dapat dipilih melalui Layer.
- Field Konten yang dipilih menampilkan nilai terbaru; perubahan segera tercermin di canvas.
- Perubahan teks tidak menghapus markup sibling atau struktur template.
- Teks pendek, panjang, multi-baris, dan karakter khusus tidak menyebabkan overlap yang tidak disengaja.
- Bounding box mengikuti teks yang terlihat setelah perubahan konten/font/ukuran/layout.

### 2.3 Editing gambar

- Upload gambar berhasil dan memperbarui canvas.
- URL gambar valid memperbarui canvas.
- URL/data tidak valid ditangani tanpa membuat editor crash.
- Foto Bawaan mengembalikan aset embedded asli.
- Crop/Fit, zoom, geser horizontal/vertikal, opacity, ukuran frame, dan reset crop bekerja pada elemen burger yang benar.
- Perubahan gambar tidak mengubah posisi teks atau footer.

### 2.4 Editing dekorasi

- Delapan shape/dekorasi tersedia di Layer.
- Shape yang punya area visual dapat dipilih langsung di canvas jika tidak mengganggu hitbox lain.
- Background dan shade yang menutupi canvas tetap dipilih melalui Layer, tidak boleh menangkap seluruh pointer canvas.
- Warna, opacity, border, radius, posisi/ukuran/rotasi yang ditampilkan harus bekerja sesuai tipe target.
- Reset style mengembalikan CSS original, termasuk gradasi dan garis pemisah.

### 2.5 Panel Desain

Untuk teks: font, ukuran, ketebalan, italic, uppercase, line-height, letter-spacing, alignment, warna teks HEX, warna latar, posisi X/Y, lebar, tinggi, rotasi, opacity, radius, border, shadow jika tersedia.

Untuk gambar: ganti foto, Crop/Fit, zoom, offset X/Y, opacity, posisi, ukuran, rotasi, reset crop.

Untuk shape: warna latar, opacity, posisi, ukuran, rotasi, border/radius jika relevan, reset style.

Tidak boleh menampilkan kontrol seolah-olah berfungsi jika renderer tidak mengaplikasikan propertinya. Bila suatu properti tidak relevan untuk tipe elemen, kontrol itu tidak perlu ditampilkan.

### 2.6 Riwayat dan ekspor

- Perubahan konten/style/geometri dicatat pada history.
- Undo mengembalikan satu perubahan dan redo mengembalikan perubahan itu lagi.
- Pemilihan elemen tidak membuat perubahan desain palsu pada history.
- Pindah halaman dan kembali tidak kehilangan state.
- Export Current dan Export All mempertahankan konten, style, gambar, dan layout yang tersimpan.
- Template Classic, Isi, dan Langkah Memasak tetap bekerja seperti sebelumnya.

## 3. Checklist eksekusi — urutan wajib

### Fase A — Baseline dan validasi kontrak

- [x] A1. Catat SHA baseline source dan dokumen sebelum edit.
- [ ] A2. Buat pemeriksaan otomatis untuk keunikan ID kontrak, keunikan `contentKey` teks, keberadaan selector dan geometri, jumlah kemunculan selector tepat satu, serta label Layer untuk semua 28 elemen.
- [x] A3. Pastikan setiap `contentKey` memiliki nilai default yang benar dan setiap field editor menunjuk ke key yang sama dengan kontrak.
- [x] A4. Pastikan selector teks tetap menunjuk ke leaf node; tandai parent/group/background sebagai non-text.
- [ ] A5. Perbaiki validasi runtime: kegagalan selector/model harus menghasilkan diagnostic yang dapat ditemukan, tidak boleh diam-diam menghilangkan target dari UI produksi.
- [ ] A6. Pastikan semua elemen dapat dijangkau lewat Layer; background/shade tetap tidak menangkap klik canvas.

### Fase B — Renderer, geometri, dan selection

- [ ] B1. Audit konversi koordinat HTML iframe → template px → A4 canvas; dokumentasikan rumus dan skala tunggal yang dipakai.
- [ ] B2. Audit hitbox untuk 28 elemen pada ukuran canvas normal, zoom editor 50%, 75%, 100%, dan Fit.
- [ ] B3. Pastikan pengukuran diulang setelah font selesai dimuat, konten berubah, style berubah, image load, dan iframe/canvas resize.
- [ ] B4. Pastikan tidak ada hitbox nol ukuran untuk elemen visual yang harus bisa dipilih.
- [ ] B5. Pastikan hitbox teks bertingkat/berdekatan tidak saling menutupi secara tidak sengaja.
- [ ] B6. Pastikan drag, resize, rotasi, alignment, dan z-order mengubah node serta hitbox pada target yang sama.
- [ ] B7. Pastikan selection overlay mengikuti elemen yang terlihat setelah setiap perubahan tanpa offset kumulatif.

### Fase C — Panel Konten dan data

- [ ] C1. Audit semua 19 field teks terhadap contract ID, `contentKey`, nilai awal, label, dan node render.
- [ ] C2. Pastikan setiap field hanya mengubah key miliknya; perubahan tidak menimpa nilai elemen lain.
- [ ] C3. Uji teks kosong, pendek, panjang, multi-baris, tanda kutip, ampersand, tanda baca, dan karakter Indonesia.
- [ ] C4. Pastikan gambar bisa di-upload dan URL gambar bisa diedit.
- [ ] C5. Pastikan Foto Bawaan memulihkan sumber embedded original.
- [ ] C6. Pastikan kegagalan load gambar memberi hasil yang terkendali dan tidak merusak canvas.
- [ ] C7. Pastikan shape/dekorasi menjelaskan bahwa pengaturan dilakukan melalui tab Desain tanpa field teks palsu.

### Fase D — Panel Desain dan style mapping

- [ ] D1. Buat matriks property → kontrol UI → state key → properti DOM/CSS yang diterapkan untuk text, image, dan shape.
- [ ] D2. Verifikasi font family khusus template dan font umum.
- [ ] D3. Verifikasi font size, weight, italic, uppercase, line-height, letter-spacing, dan alignment.
- [ ] D4. Verifikasi warna teks, HEX, warna latar, opacity, border, radius, dan shadow jika ditampilkan.
- [ ] D5. Verifikasi X/Y, width/height, rotasi, alignment, dan layer order.
- [ ] D6. Verifikasi image fit, zoom, offset, opacity, ukuran frame, dan reset crop.
- [ ] D7. Verifikasi reset style mengembalikan CSS template asli dan menghapus override terkait tanpa menghapus konten.
- [ ] D8. Hilangkan atau perbaiki kontrol yang tidak punya jalur penerapan ke renderer; jangan membiarkan kontrol tampak aktif tetapi tidak berfungsi.

### Fase E — Stabilitas layout deskripsi

- [ ] E1. Uji setiap bagian deskripsi waktu secara individual.
- [ ] E2. Uji teks pendek dan panjang pada label waktu, durasi, feature line, feature prefix, dan feature emphasis.
- [ ] E3. Uji perubahan font family, font size, line-height, letter-spacing, width, dan alignment satu per satu.
- [ ] E4. Pastikan tidak ada teks bertumpuk, terpotong, tertutup, atau hitbox yang tertinggal dari posisi teks.
- [ ] E5. Pastikan layout kembali stabil setelah reset style.
- [ ] E6. Jika overlap terkonfirmasi, perbaiki akar penyebab DOM/CSS/measurement; jangan menambahkan offset koordinat khusus yang hanya cocok untuk screenshot.

### Fase F — History, lifecycle, dan regresi

- [ ] F1. Verifikasi perubahan konten masuk ke undo/redo.
- [ ] F2. Verifikasi perubahan style/geometri masuk ke undo/redo.
- [ ] F3. Verifikasi memilih elemen dan pengukuran ulang tidak membuat entri history palsu.
- [ ] F4. Pindah halaman, kembali ke Double Smash, dan pastikan data/style tetap.
- [ ] F5. Duplikasi halaman Double Smash dan pastikan state independen.
- [ ] F6. Verifikasi lifecycle iframe: load awal, ganti halaman, unmount, reload, dan resize tidak meninggalkan listener/observer.
- [ ] F7. Jalankan pemeriksaan regresi Cover Classic, Isi, dan Langkah Memasak.

### Fase G — Test dan bukti

- [ ] G1. Jalankan install/build sesuai lockfile dan script di package.json.
- [ ] G2. Jalankan lint/typecheck/test yang memang tersedia di repository.
- [ ] G3. Tambahkan/eksekusi automated tests untuk kontrak selector dan mapping yang dapat diuji tanpa browser.
- [ ] G4. Jalankan browser test pada viewport desktop dan viewport rendah; jangan mengganti browser test dengan pembacaan source.
- [ ] G5. Uji 28 elemen melalui canvas dan Layer, panel Konten/Desain, teks panjang, gambar, dekorasi, drag/resize, undo/redo, dan export.
- [ ] G6. Catat hasil aktual, error, commit SHA, dan batas verifikasi. Jangan menyatakan lulus jika tidak bisa menjalankan test.
- [ ] G7. Pastikan semua perubahan kode berada di `main`; AI tidak melakukan deployment.

### Fase H — Handoff untuk owner (satu-satunya fase deploy)

- [ ] H1. Berikan commit SHA dan ringkasan perubahan yang sudah lolos pengujian lokal.
- [ ] H2. Owner melakukan deployment sendiri.
- [ ] H3. Owner membuka URL produksi dan memverifikasi cover Double Smash terbaru.
- [ ] H4. Owner menguji kembali teks deskripsi, 19 field teks, gambar, dekorasi, panel Konten/Desain, undo/redo, dan export.
- [ ] H5. Checklist hanya ditutup setelah hasil lokal yang relevan dan verifikasi pascadeploy owner dilaporkan; AI tidak mengasumsikan deploy sukses.

## 4. Format bukti wajib per item

Untuk setiap item yang dicentang, catat minimal:
- Item ID.
- Status: PASS / FAIL / BLOCKED.
- Metode: static check / automated test / build / browser / owner production.
- Bukti: output test, log, URL/commit SHA, atau langkah reproduksi.
- Jika gagal: gejala, akar penyebab yang terbukti, dan commit perbaikannya.

Jika lingkungan tidak menyediakan tool untuk menjalankan browser, tandai item browser sebagai BLOCKED dan jelaskan batasnya. Jangan mengubahnya menjadi PASS melalui inspeksi source.

## 5. Referensi teknis

- MDN — `Element.getBoundingClientRect()`: posisi/ukuran relatif viewport dan pengaruh scrolling. https://developer.mozilla.org/en-US/docs/Web/API/Element/getBoundingClientRect
- MDN — Resize Observer API: mengamati perubahan ukuran elemen, termasuk perubahan yang tidak disebabkan window resize. https://developer.mozilla.org/en-US/docs/Web/API/Resize_Observer_API
- W3C WCAG 2.2 — Target Size (Minimum), 24 × 24 CSS px dengan pengecualian yang ditentukan standar. Gunakan sebagai pedoman untuk kontrol editor, bukan untuk memaksakan ukuran hitbox teks pada desain cetak. https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html

## 6. Batas selesai

Pekerjaan kode baru dapat disebut siap untuk owner deploy setelah fase A–G lulus atau setiap BLOCKED disertai alasan teknis yang nyata dan disetujui owner. Pekerjaan end-to-end baru dapat disebut selesai setelah owner menyelesaikan H2–H4. AI tidak boleh mengklaim status production berdasarkan commit atau status build saja.
