# SILIT — Audit dan Checklist Terkunci: Cover Double Smash Cheeseburger

**Dokumen:** audit teknis + spesifikasi implementasi  
**Repositori aplikasi:** `omegasands87/silit`  
**Repositori dokumentasi:** `omegasands87/silitdoc`  
**Branch kerja aplikasi:** `main`  
**Tanggal audit:** 10 Oktober 2026  
**Status:** Spesifikasi dikunci; pekerjaan implementasi wajib mengikuti urutan dan kriteria di bawah.  
**Batas tanggung jawab:** AI mengaudit, mengubah kode, menjalankan build/pengujian yang tersedia, dan mencatat bukti. User melakukan deployment. AI tidak melakukan deploy.

---

## 0. Aturan penguncian spesifikasi

1. Dokumen ini adalah kontrak kerja untuk perbaikan cover Double Smash Cheeseburger.
2. Scope, urutan kerja, dan acceptance criteria di dokumen ini tidak boleh diubah secara diam-diam setelah dokumen dibuat.
3. Jika implementasi menemukan masalah yang sudah tercakup secara substansi dalam kriteria di bawah, selesaikan dalam scope ini tanpa meminta persetujuan ulang.
4. Jangan menambah fitur yang tidak diperlukan untuk memenuhi kriteria ini.
5. Jika ada hambatan teknis, jangan menghapus atau melonggarkan kriteria agar pekerjaan terlihat selesai. Catat hambatan dan bukti pada laporan eksekusi terpisah.
6. Status checklist hanya boleh ditandai selesai setelah bukti pemeriksaan yang disebutkan tersedia. Commit bukan bukti bahwa browser behavior berhasil.
7. Semua perubahan aplikasi langsung ke branch `main`, sesuai aturan proyek. Jangan deploy.
8. Jangan mengubah desain dasar Double Smash, aset gambar tertanam, atau font tertanam kecuali perubahan spesifik diperlukan untuk memenuhi kriteria dan menjaga desain asli.
9. Jangan mengubah halaman Cover Classic, Isi, atau Langkah Memasak kecuali untuk perbaikan shared component yang diperlukan; setiap shared change wajib diuji regresinya.
10. Dokumen checklist ini menjadi baseline tetap. Perkembangan pelaksanaan dicatat pada laporan terpisah; jangan menulis ulang persyaratan checklist untuk menyesuaikan hasil implementasi.

---

## 1. Scope

Fokus pekerjaan adalah seluruh sistem editing untuk halaman cover yang menggunakan template `double-smash-cheeseburger`, meliputi:

- Kontrak elemen dan data konten.
- HTML dan CSS sumber template.
- Pemetaan source selector ke model elemen.
- Daftar Layer dan pemilihan melalui canvas.
- Hitbox transparan, geometri, drag, resize, rotasi, alignment, dan z-order.
- Panel Konten.
- Panel Desain, termasuk tipografi, warna HEX, posisi/ukuran, opacity, border, shadow, dan kontrol gambar.
- Sinkronisasi state, rendering, undo/redo, perpindahan halaman, dan ekspor/print.
- Regresi pada tiga page type Classic: Cover, Isi, dan Langkah Memasak.
- Dokumentasi dan checklist.

Tidak termasuk: deployment oleh AI, backend/database baru, redesign menyeluruh dari estetika Double Smash, perubahan template resep lain yang tidak diperlukan, dan fitur yang tidak disebutkan di sini.

---

## 2. Baseline audit yang sudah diperiksa

Source yang diperiksa dari `main` pada saat audit:

- `recipe_generator_template_editor.tsx` — blob SHA `a2dd0256858fc689bbc87a390d46e10dbce43717`
- `public/templates/cover-double-smash-cheeseburger.html` — blob SHA `e142d4f943f2ec3357c2d6b8a3c8e50055e835bd`
- `src/index.css` — blob SHA `cceb68f5494637e438d2f3766c3fa9e7d979ddb4`
- `package.json` — React 18 + Vite 6; script build adalah `vite build`.
- `silit_visual_editor_checklist.md` dan `silit_ai_mandatory_rules.md` pada repo dokumentasi.

Template HTML membawa aset font dan gambar tertanam. Aset ini harus dipertahankan.

### 2.1 Arsitektur aktual

1. Double Smash tidak dirender menggunakan komponen Cover Classic. Template asli dimuat dalam `iframe` melalui `HTMLCoverPage`.
2. Canvas menempatkan `html-cover-interaction-layer` di atas iframe. Setiap elemen yang didefinisikan kontrak mendapat hitbox berdasarkan `getBoundingClientRect()`.
3. Perubahan konten dan style diaplikasikan pada DOM iframe dari `page.data`, `page.elements`, dan `page.elementStyles`.
4. `TEMPLATE_ELEMENT_CONTRACT` mendefinisikan 20 elemen saat ini. `normalizeElements` membuat model elemen; `DoubleSmashContentEditor` membuat field Konten; `VisualElementEditor` menjadi panel Desain generik.
5. Selector layout/posisi utama berasal dari CSS template dengan basis artwork 768 × 1086.1714 px dan A4 portrait. Ukuran/posisi tidak boleh ditebak dari screenshot; harus berasal dari DOM yang terukur.

### 2.2 Pemetaan kontrak elemen saat audit

| ID | Tipe | Content key | Source selector | Temuan audit awal |
|---|---|---|---|---|
| `burger-image` | image | `burgerImage` | `.cover-photo` | Frame adalah div, gambar ada di child img; kontrol crop/fit/zoom harus konsisten dengan CSS cutout. |
| `cover-shade` | shape | — | `.cover-shade` | Hitbox sengaja tidak menangkap klik canvas; harus tetap dapat dipilih lewat Layer. Warna shape mengganti gradient asli. |
| `masthead-label` | text | `category` | `.cover-masthead p` | Target selector adalah paragraf yang juga berisi dekorasi span. Konten update harus mempertahankan span dekoratif. |
| `title-primary` | text | `titlePrimary` | `.cover-hero h1 span:nth-child(1)` | Target text leaf; selector harus tetap unik. |
| `title-secondary` | text | `titleSecondary` | `.cover-hero h1 span:nth-child(2)` | Target text leaf; selector harus tetap unik. |
| `intro-line-1` | text | `introLine1` | `.cover-intro span:nth-child(1)` | Target anak di dalam paragraf intro. |
| `intro-line-2-prefix` | text | `introLine2Prefix` | `.cover-intro span:nth-child(2)` | Selector menunjuk span yang juga berisi strong protein; style parent dapat diwariskan ke emphasis. |
| `intro-protein-emphasis` | text | `proteinEmphasis` | `.cover-intro strong` | Elemen anak bertumpang tindih dengan hitbox intro line 2; inheritance perlu diuji. |
| `time-label` | text | `timeLabel` | `.cover-time-story > span` | **Masalah terkonfirmasi:** selector menunjuk wrapper yang juga memuat `em` durasi; hitbox dan sebagian style tidak terisolasi. |
| `time-emphasis` | text | `timeEmphasis` | `.cover-time-story em` | Elemen anak bertumpang tindih dengan hitbox time-label. |
| `feature-line-1` | text | `featureLine1` | `.cover-time-story > span.silit-feature-line` | Node tidak ada di HTML sumber; dibuat dinamis oleh `HTMLCoverPage`. Lifecycle, selector, dan layout harus deterministik. |
| `feature-line-2-emphasis` | text | `featureEmphasis` | `.cover-time-story strong` | Selector ada di sumber; harus tetap terpisah dari baris pertama dan dapat diukur setelah perubahan teks. |
| `footer-prep-label` | text | `prepLabel` | `.cover-footer > div:nth-child(1) span` | Elemen leaf; harus tetap di kolom Persiapan. |
| `footer-prep-value` | text | `prepValue` | `.cover-footer > div:nth-child(1) strong` | Elemen leaf; harus tetap di kolom Persiapan. |
| `footer-cooking-label` | text | `cookingLabel` | `.cover-footer > div:nth-child(2) span` | Elemen leaf; harus tetap di kolom Memasak. |
| `footer-cooking-value` | text | `cookingValue` | `.cover-footer > div:nth-child(2) strong` | Elemen leaf; harus tetap di kolom Memasak. |
| `footer-calorie-label` | text | `calorieLabel` | `.cover-footer > div:nth-child(3) span` | Elemen leaf; harus tetap di kolom Kalori. |
| `footer-calorie-value` | text | `calorieValue` | `.cover-footer > div:nth-child(3) strong` | Elemen leaf; harus tetap di kolom Kalori. |
| `footer-portion-label` | text | `portionLabel` | `.cover-footer > div:nth-child(4) span` | Elemen leaf; harus tetap di kolom Porsi. |
| `footer-portion-value` | text | `portionValue` | `.cover-footer > div:nth-child(4) strong` | Elemen leaf; harus tetap di kolom Porsi. |

**Catatan:** 20 adalah jumlah definisi saat audit, bukan bukti bahwa semua target berfungsi sempurna. Semua selector harus diperiksa saat runtime; selector dinamis harus diverifikasi setelah node dibuat.

---

## 3. Temuan audit teknis

### A. Konten dan struktur DOM

- `applyDoubleSmashContent` menggunakan `textContent` untuk kebanyakan target dan fungsi khusus `setFirstTextNode` untuk `masthead-label`, `intro-line-2-prefix`, serta `time-label`. Pola khusus ini harus dipertahankan atau diganti dengan mekanisme terstruktur yang lebih aman; jangan meratakan child markup yang masih diperlukan.
- `time-label` menunjuk parent span yang membungkus `em` berisi durasi. Karena target edit parent juga mencakup child, batas seleksi dan sebagian properti typography berpotensi bocor ke elemen durasi.
- `intro-line-2-prefix` menunjuk span yang membungkus kata pengantar sekaligus strong protein. Properti yang diwariskan (misalnya font family, size, color, letter spacing, atau line-height) dapat memengaruhi emphasis meskipun child mempunyai sebagian aturan sendiri.
- `feature-line-1` ditambahkan ke iframe dengan memindahkan text node sebelum `br` ke span buatan. Ini harus diuji terhadap rerender, penggantian teks, perubahan font, pergantian halaman, dan pemuatan iframe ulang.
- Panel Konten menampilkan field sesuai elemen terpilih; tanpa pilihan, semua field kontrak ditampilkan. Pastikan setiap elemen teks punya field yang tepat, gambar punya alur penggantian yang jelas, dan dekorasi memiliki penjelasan yang benar.
- Update teks yang lebih panjang/pendek harus memicu pengukuran ulang hitbox setelah browser selesai melakukan layout, bukan menggunakan geometri lama.

### B. Selector, geometri, dan pemilihan

- `HTMLCoverPage` mengukur hitbox dari `definition.sourceSelector`; metadata `geometryRef` pada kontrak tidak digunakan untuk mengukur hitbox saat ini. Implementasi harus memiliki satu aturan geometri yang eksplisit dan konsisten.
- Hitbox saat ini berasal dari bounding box elemen DOM yang dipilih. Untuk selector parent yang memuat child editable, hitbox tumpang tindih. Tumpang tindih ini harus diselesaikan, bukan hanya ditutupi dengan z-index.
- Pengukuran mengubah koordinat iframe ke koordinat canvas dengan `frameScale` dan `canvasScale`. Harus diuji pada zoom 50%, 75%, 100%, Fit, resize viewport, dan perubahan ukuran sidebar.
- `cover-shade` memiliki `pointer-events: none`; pilih melalui Layer harus tetap berfungsi. Elemen dekoratif tidak boleh menutupi hitbox teks/gambar.
- Urutan Layer memakai `zIndex` model, sedangkan template HTML memiliki parent/stacking context CSS. Verifikasi apakah semua aksi Paling depan/Naik/Turun/Paling belakang benar-benar menghasilkan urutan visual yang sesuai; jangan menganggap perubahan angka z-index cukup.
- Tombol/handle selection overlay, hitbox, dan panel harus selalu mengacu ke ID elemen yang sama. Seleksi tidak boleh berubah ke elemen lain saat area hitbox tumpang tindih.

### C. Panel Desain dan sinkronisasi style

- `VisualElementEditor` generik digunakan untuk teks, gambar, shape, dan group. Semua kontrol yang terlihat harus benar-benar memengaruhi node template yang benar.
- Model `page.elements[].x/y/width/height/rotation` dan `page.elementStyles[key]` adalah dua sumber data yang perlu dijaga sinkron. Posisi di panel harus tetap sesuai dengan drag/resize dan tidak kembali ke nilai lama ketika panel dirender ulang.
- Font pilihan panel mencakup Default, Inter, Playfair Display, Arial, Georgia, dan Times New Roman; template memakai font tertanam khusus. Default harus mempertahankan font sumber; pilihan font lain harus bekerja hanya pada elemen terpilih dan tidak menghapus struktur teks.
- Line-height dan letter-spacing harus menerima nilai valid dan menampilkan nilai yang konsisten saat elemen dipilih ulang.
- HEX sudah tersedia untuk warna teks dan background generik, tetapi kontrol warna border masih menggunakan native color picker saja. Samakan kemampuan input HEX di seluruh kontrol warna yang terlihat pada panel Double Smash.
- `backgroundColor` pada shape `cover-shade` secara sengaja menghilangkan background-image/gradient. UI harus memberi tahu dampaknya; reset harus mengembalikan gaya sumber template.
- Kontrol posisi/ukuran harus mengubah posisi dan ukuran node sebenarnya. Ukuran auto/kosong harus dapat dipulihkan; resize manual tidak boleh membuat teks atau foto keluar dari halaman.
- Kontrol opacity, border radius, border width/color, shadow, alignment, rotation, dan z-order harus diuji untuk setiap tipe elemen yang relevan.
- Reset gaya harus mengembalikan style/geometry ke default template tanpa menghapus konten pengguna, gambar pengganti, atau data halaman.
- Panel gambar menampilkan Fit/Crop, zoom, offset, dan Reset Crop. Nilai default visual saat ini adalah `contain` untuk `burger-image`, sedangkan fungsi reset menetapkan `objectFit: cover`; default dan reset tidak konsisten dan harus diselaraskan. Pastikan reset hanya mengatur crop, bukan mengganti sumber gambar.
- Transform zoom/offset harus memberi hasil yang intuitif dan tidak menggeser foto keluar dari frame tanpa cara mengembalikannya.

### D. Template CSS dan aset

- CSS sumber mempunyai beberapa deklarasi berulang untuk `.cover-page`, `.cover-artwork`, `.cover-photo`, dan `.cover-change`. Sebagian dapat merupakan aturan print/responsive yang disengaja; jangan menghapusnya secara membabi buta. Audit urutan cascade dan bedakan aturan layar, print, dan export.
- `.cover-time-story > span` menetapkan display, margin, font, dan line-height pada semua span anak langsung. Span `.silit-feature-line` buatan mempunyai inline override untuk sebagian properti; verifikasi computed style, line wrapping, dan tinggi hasil akhir.
- Template menggunakan `.cover-photo-cutout img` dengan `object-fit: contain`, drop-shadow, serta ukuran/posisi khusus. Kontrol gambar harus mempertahankan cutout dan tidak mengasumsikan foto bulat/crop standar.
- Background artwork adalah radial gradient, sedangkan `.cover-shade` menambahkan beberapa gradient. Pengaturan background shape harus jelas bahwa mengganti warna menghapus gradient asli pada shade.
- Font dan gambar embedded adalah aset sumber. Jangan menghapus atau mengubah base64 karena alasan refactor, ukuran file, atau formatting.
- CSS template mencakup aturan print. Canvas dan hasil print/export harus mempertahankan ukuran A4, font, background, gambar, dan posisi.

### E. State, undo/redo, dan export

- Perubahan konten/style harus hanya memengaruhi page ID aktif, bukan semua halaman yang memakai template sama.
- Duplikasi halaman harus mengkloning data/style tanpa membuat perubahan di satu salinan memengaruhi salinan lain.
- Undo/redo harus mencakup perubahan teks, style, drag, resize, alignment, crop, dan reset.
- Export Current dan Export All masuk ke print mode; verifikasi iframe content dan styling muncul di hasil ekspor/print dan overlay editor tidak ikut tercetak.
- Perubahan DOM iframe harus idempotent: rerender tidak boleh menggandakan node dinamis, menumpuk inline style, atau merusak struktur HTML.
- Perpindahan page type dan unmount/remount iframe tidak boleh mempertahankan selection/hitbox yang stale.

---

## 4. Checklist implementasi terkunci

**Semua item di bawah wajib dikerjakan berurutan.** Status pada dokumen ini dimulai belum selesai; status hanya dapat diubah setelah bukti sesuai tersedia.

### CHECKLIST A — Kontrak dan diagnostik elemen

- [ ] A1. Audit 20 definisi kontrak terhadap node DOM saat runtime; catat selector yang tidak ditemukan, tidak unik, atau tidak sesuai jenis node.
- [ ] A2. Tetapkan satu sumber kebenaran untuk element ID, selector, label Layer, field Konten, tipe, dan kontrol Desain.
- [ ] A3. Hilangkan selector parent/child yang tumpang tindih untuk elemen yang dimaksudkan bisa diedit terpisah, khususnya time label vs time emphasis dan intro prefix vs protein emphasis.
- [ ] A4. Pastikan dekorasi yang penting (garis aksen masthead, separator intro, dan separator footer bila memang bagian visual mandiri) memiliki kontrol/seleksi yang masuk akal; jangan membuat node edit palsu yang merusak layout.
- [ ] A5. Tentukan dan implementasikan aturan `geometryRef` atau hapus ketergantungan semu padanya secara konsisten dalam kode; geometri harus diukur, bukan ditebak.
- [ ] A6. Tambahkan diagnostik development yang jelas bila selector elemen yang wajib tidak ditemukan; tidak boleh diam-diam melewati elemen penting.

### CHECKLIST B — Struktur teks dan layout

- [ ] B1. Buat mekanisme teks deskripsi yang stabil dan terstruktur; hindari manipulasi text node yang rapuh jika struktur render dapat dinyatakan secara eksplisit.
- [ ] B2. Semua potongan teks yang dimaksudkan mandiri harus dapat dipilih tanpa mengambil area anak lain.
- [ ] B3. Style pada satu potongan teks tidak boleh mengubah sibling atau child lain kecuali properti memang sengaja diwariskan dan didokumentasikan.
- [ ] B4. Ubah teks menjadi lebih pendek/panjang dan verifikasi tidak ada tumpang tindih dengan judul, gambar, atau footer.
- [ ] B5. Setelah update konten/font/ukuran/line-height/letter-spacing, ukur ulang hitbox setelah layout stabil.
- [ ] B6. Pastikan node dinamis seperti feature line tidak digandakan saat rerender atau pergantian halaman.
- [ ] B7. Pertahankan copy, font, warna, gradient, gambar, dan komposisi dasar Double Smash kecuali penyesuaian yang diperlukan untuk menghilangkan bug.

### CHECKLIST C — Panel Konten

- [ ] C1. Semua teks yang tercantum dalam kontrak memiliki field Konten dengan label yang jelas.
- [ ] C2. Setiap field mengubah hanya content key yang dimaksud dan hasilnya muncul pada canvas tanpa menghilangkan markup sibling.
- [ ] C3. Gambar burger dapat diganti, tetap mempertahankan sumber embedded sampai pengguna menggantinya, dan tidak rusak setelah undo/redo.
- [ ] C4. Dekorasi menjelaskan bahwa tidak memiliki teks dan pengaturan visual tersedia pada tab Desain.
- [ ] C5. Seleksi dari canvas dan Layer membuka elemen yang sama; field Konten tetap dapat diakses setelah berpindah tab.
- [ ] C6. Saat tidak ada elemen terpilih, semua field tersedia dalam grup yang jelas dan tidak ada field kontrak yang hilang.
- [ ] C7. Tidak ada field yang ditampilkan untuk selector tidak valid tanpa diagnostik yang dapat ditindaklanjuti.

### CHECKLIST D — Panel Desain

- [ ] D1. Font default mempertahankan font sumber per elemen; pilihan font mengubah hanya elemen terpilih.
- [ ] D2. Ukuran font, ketebalan, italic, line-height, letter-spacing, transform teks, alignment, dan warna teks bekerja secara independen.
- [ ] D3. Semua kontrol warna yang tersedia pada panel termasuk warna border mendukung picker dan HEX `#RRGGBB`; input invalid tidak diterapkan.
- [ ] D4. Warna latar teks dan warna shade tidak menimpa elemen lain; perilaku penggantian gradient dijelaskan.
- [ ] D5. X/Y, lebar, tinggi, rotasi, alignment, opacity, radius, border, shadow, dan urutan layer terhubung ke model dan render yang benar.
- [ ] D6. Nilai di panel cocok dengan geometri yang tampak setelah drag/resize dan saat elemen dipilih ulang.
- [ ] D7. Reset gaya mengembalikan gaya template dan geometry default tanpa menghapus konten/gambar pengganti.
- [ ] D8. Kontrol Fit/Crop, zoom, offset X/Y, dan Reset Crop konsisten dengan default CSS `cover-photo-cutout`; reset tidak mengganti image source.
- [ ] D9. Kontrol yang tidak berlaku untuk tipe elemen tertentu tidak ditampilkan atau diberi penjelasan, bukan tampak aktif tetapi tidak bekerja.
- [ ] D10. Gaya elemen tidak bocor ke elemen parent, child, atau sibling.

### CHECKLIST E — Hitbox, geometri, dan layer

- [ ] E1. Hitbox mengikuti batas visual elemen yang dipilih dan tidak mengambil area teks lain.
- [ ] E2. Pemilihan melalui canvas dan Layer selalu menghasilkan ID dan tipe yang sama.
- [ ] E3. Drag, multi-select, resize handle, rotasi, snapping, alignment, dan z-order berfungsi pada semua elemen yang relevan.
- [ ] E4. Dekorasi shade bisa dipilih dari Layer dan tidak menghalangi klik elemen yang berada di atasnya.
- [ ] E5. Uji skala 50%, 75%, 100%, Fit, serta resize viewport/sidebar; hitbox tetap tepat.
- [ ] E6. Layout berubah setelah teks/style berubah dan overlay tidak tertinggal pada posisi lama.
- [ ] E7. Aksi z-order menghasilkan urutan visual yang benar meskipun DOM memiliki parent dan stacking context.
- [ ] E8. Tidak ada hitbox zero-size, di luar halaman tanpa sengaja, atau tertinggal setelah iframe reload.

### CHECKLIST F — State dan integritas dokumen

- [ ] F1. Edit cover Double Smash hanya memengaruhi halaman aktif.
- [ ] F2. Duplikasi halaman mengkloning konten, image, geometry, dan style secara independen.
- [ ] F3. Undo/redo mengembalikan teks, gaya, posisi, ukuran, crop, dan reset secara benar.
- [ ] F4. Perpindahan halaman tidak mempertahankan selected element atau hitbox stale.
- [ ] F5. Rerender idempotent dan tidak menggandakan span atau mengakumulasi inline style.
- [ ] F6. Data template seed/asli tidak berubah akibat edit instance halaman.

### CHECKLIST G — Build dan pengujian regresi

- [ ] G1. Build produksi `npm run build` berhasil.
- [ ] G2. Pengujian browser Double Smash untuk setiap elemen kontrak: pilih dari Layer, ubah konten/style, pilih ulang, undo/redo.
- [ ] G3. Pengujian browser untuk deskripsi pendek/panjang, font fallback, warna HEX, gambar/crop, resize, alignment, dan layer order berhasil.
- [ ] G4. Export Current dan Export All mempertahankan template, gambar, font, ukuran A4, serta tidak menyertakan hitbox/toolbar.
- [ ] G5. Regresi Cover Classic: pemilihan individual, Konten, Desain, HEX, posisi/ukuran, gambar, undo/redo, export.
- [ ] G6. Regresi Isi: judul cerita, bahan, alat, nutrisi, footer, add/remove item, style individual, undo/redo, export.
- [ ] G7. Regresi Langkah Memasak: judul, tiap judul/deskripsi langkah, Pro Tip, pagination, add/remove item, style individual, undo/redo, export.
- [ ] G8. Tidak ada perubahan pada fitur halaman tambah/duplikasi/hapus/pindah halaman.
- [ ] G9. Semua bukti hasil build dan pengujian dicatat dalam laporan eksekusi terpisah.
- [ ] G10. Berhenti sebelum deployment. Berikan commit SHA dan instruksi ringkas agar user dapat melakukan deploy sendiri.

---

## 5. Definisi selesai

Pekerjaan hanya dapat dinyatakan selesai bila:

1. Semua item checklist A–G telah memiliki bukti keberhasilan, kecuali langkah deployment yang memang menjadi tanggung jawab user.
2. Tidak ada selector wajib yang hilang atau tidak terdiagnosis.
3. Semua elemen yang dijanjikan dapat dipilih dan dikendalikan melalui panel yang sesuai.
4. Konten dan style tidak bocor antarelemen.
5. Hasil canvas dan hasil export/print konsisten.
6. Build dan seluruh uji regresi lulus.
7. Perubahan kode ada di branch `main`, tidak ada deploy yang dilakukan AI.

Jika browser automation tidak tersedia, jangan mengklaim pengujian browser selesai. Gunakan pengujian manual yang bisa dijalankan dalam sandbox/preview lokal dan dokumentasikan batasan yang masih tersisa.

## 6. Laporan eksekusi

Catatan kemajuan, commit SHA, hasil build, hasil tes, dan kendala ditulis pada dokumen laporan terpisah. Dokumen ini tidak digunakan untuk menulis ulang atau melonggarkan persyaratan.
