# SILIT --- DOKUMENTASI CHECKLIST PEKERJAAN

## Visual Recipe Editor

**Status:** Rencana kerja terkunci\
**Tanggal:** 8 Oktober 2026

------------------------------------------------------------------------

## 1. ATURAN WAJIB

Dokumen ini adalah checklist kerja yang menjadi batas pekerjaan.

### 1.1 Scope terkunci

Pekerjaan hanya boleh mengikuti urutan pada dokumen ini.

Tidak boleh: - menambah fitur di luar checklist; - mengubah fitur yang
tidak termasuk pekerjaan; - mengubah desain atau perilaku yang tidak
diperlukan oleh checklist; - menambahkan backend, database, storage,
atau layanan lain; - mengembangkan pekerjaan ke arah lain tanpa
persetujuan.

### 1.2 Jika ditemukan kebutuhan di luar checklist

Pekerjaan harus berhenti.

Sebelum mengubahnya harus dijelaskan: 1. masalahnya; 2. alasan perubahan
diperlukan; 3. bagian checklist yang terdampak; 4. perubahan yang akan
dilakukan.

Lanjut hanya setelah mendapat persetujuan.

### 1.3 Bagian yang wajib dipertahankan

-   Data resep yang sekarang.
-   Page type:
    -   Cover
    -   Isi
    -   Langkah Memasak
-   Add Page.
-   Duplicate Page.
-   Delete Page.
-   Move Page.
-   Page selection.
-   Editor data resep yang sudah ada.
-   Upload gambar.
-   Tampilan dasar desain resep.

Perubahan hanya dilakukan jika memang diperlukan oleh checklist.

------------------------------------------------------------------------

# 2. URUTAN PEKERJAAN

## CHECKLIST 01 --- Stabilkan Struktur Editor

### Pekerjaan

-   ✅ Pisahkan model halaman dan elemen.
-   ✅ Page tetap memiliki `id`, `type`, dan `data`.
-   ✅ Tambahkan model `elements[]` untuk elemen visual.
-   ✅ Setiap elemen memiliki minimal:
    -   ✅ `id`
    -   ✅ `type`
    -   ✅ `content`
    -   ✅ `x`
    -   ✅ `y`
    -   ✅ `width`
    -   ✅ `height`
    -   ✅ `rotation`
    -   ✅ `zIndex`
    -   ✅ `style`
-   ✅ Data image memiliki data image yang diperlukan.

### Hasil wajib

-   Layout tidak lagi bergantung pada wrapper editor sebagai sumber
    layout utama.
-   Wrapper selection hanya menangani selection dan interaction.

### Lulus jika

-   ✅ Memilih element tidak mengubah layout.
-   ✅ Struktur visual dapat dirender dari model element.

------------------------------------------------------------------------

## CHECKLIST 02 --- Perbaiki A4

### Pekerjaan

-   [ ] Pertahankan ukuran A4: 210mm × 297mm.
-   [ ] Canvas tetap portrait.
-   [ ] Canvas memiliki background.
-   [ ] Overflow canvas terkendali.
-   [ ] Cover image kembali memiliki area 60% A4.
-   [ ] Area informasi cover tetap 40% A4.

### Hasil wajib

-   Proporsi cover sama dengan desain awal.
-   Selection editor tidak mengubah ukuran image.
-   Selection editor tidak mengubah pembagian 60% / 40%.

### Lulus jika

-   [ ] Cover image tidak mengecil karena wrapper editor.
-   [ ] Canvas tidak blank.

------------------------------------------------------------------------

## CHECKLIST 03 --- Selection Element

### Element Cover

-   [ ] Foto Sampul
-   [ ] Kategori
-   [ ] Judul
-   [ ] Kutipan
-   [ ] Meta

### Element Isi

-   [ ] Judul Cerita
-   [ ] Teks Cerita
-   [ ] Bahan
-   [ ] Alat
-   [ ] Nutrisi
-   [ ] Footer

### Element Cooking

-   [ ] Judul Memasak
-   [ ] Langkah
-   [ ] Pro Tip
-   [ ] Footer

### Interaction

-   [ ] Klik element memilih element.
-   [ ] Bounding box muncul.
-   [ ] Panel kanan menampilkan element yang dipilih.
-   [ ] Klik area kosong menghapus selection.
-   [ ] Klik area kosong tidak menyebabkan blank.

### Lulus jika

-   [ ] Semua element pada daftar dapat dipilih.
-   [ ] Selection tidak merusak layout.

------------------------------------------------------------------------

## CHECKLIST 04 --- Drag Element

### Pekerjaan

-   [ ] Element dapat di-drag langsung di canvas.
-   [ ] Posisi mengikuti mouse.
-   [ ] Posisi X/Y diperbarui.
-   [ ] Perubahan X/Y dari panel mengubah posisi element.
-   [ ] Canvas tetap stabil setelah drag.

### Lulus jika

-   [ ] Posisi canvas dan panel X/Y konsisten.
-   [ ] Element lain tidak ikut berpindah.

------------------------------------------------------------------------

## CHECKLIST 05 --- Resize Element

### Pekerjaan

-   [ ] Tambahkan handle kiri.
-   [ ] Tambahkan handle kanan.
-   [ ] Tambahkan handle atas.
-   [ ] Tambahkan handle bawah.
-   [ ] Tambahkan 4 corner handle.
-   [ ] Resize memperbarui width/height.
-   [ ] Resize tidak merusak element lain.
-   [ ] Resize tidak menyebabkan blank.

### Image

-   [ ] Frame image tetap valid.
-   [ ] Image tetap berada di dalam frame.

### Lulus jika

-   [ ] Resize dari canvas dan ukuran pada model konsisten.

------------------------------------------------------------------------

## CHECKLIST 06 --- Image Editing

### Pekerjaan

-   [ ] Replace image.
-   [ ] Crop image.
-   [ ] Position image di dalam frame.
-   [ ] Zoom image di dalam frame.
-   [ ] Fit: Cover.
-   [ ] Fit: Contain.

### Lulus jika

-   [ ] Frame tidak berubah saat image digeser.
-   [ ] Crop terlihat benar di canvas.
-   [ ] Zoom terlihat benar di canvas.
-   [ ] Position terlihat benar di canvas.
-   [ ] Hasil export mengikuti crop, zoom, dan position canvas.

------------------------------------------------------------------------

## CHECKLIST 07 --- Layer

### Pekerjaan

-   [ ] Bring Forward.
-   [ ] Send Backward.
-   [ ] Bring to Front.
-   [ ] Send to Back.
-   [ ] Tampilkan layer element halaman aktif.
-   [ ] Urutan layer panel sama dengan hasil visual canvas.

### Lulus jika

-   [ ] Perubahan layer langsung terlihat di canvas.
-   [ ] Urutan layer tidak berubah saat export.

------------------------------------------------------------------------

## CHECKLIST 08 --- Alignment

### Pekerjaan

-   [ ] Align Left.
-   [ ] Align Center.
-   [ ] Align Right.
-   [ ] Align Top.
-   [ ] Align Middle.
-   [ ] Align Bottom.
-   [ ] Center Horizontally.
-   [ ] Center Vertically.

### Lulus jika

-   [ ] Element berpindah sesuai perintah alignment.
-   [ ] Posisi hasil alignment konsisten dengan canvas.

------------------------------------------------------------------------

## CHECKLIST 09 --- Guides dan Snap

### Pekerjaan

-   [ ] Center guide.
-   [ ] Edge alignment guide.
-   [ ] Snap ke guide.
-   [ ] Snap ke element lain.

### Hasil wajib

-   Guide muncul saat diperlukan.
-   Element dapat disejajarkan dengan mudah.

### Lulus jika

-   [ ] Snap tidak memindahkan element secara tidak terduga.
-   [ ] Guide tidak ikut muncul pada hasil export.

------------------------------------------------------------------------

## CHECKLIST 10 --- Multi-Select

### Pekerjaan

-   [ ] Pilih element pertama.
-   [ ] Tambahkan element menggunakan modifier key.
-   [ ] Semua element yang dipilih terlihat.
-   [ ] Alignment dapat digunakan untuk selection.

### Lulus jika

-   [ ] Multi-select tidak merusak layout.
-   [ ] Element yang tidak dipilih tidak ikut berubah.

------------------------------------------------------------------------

## CHECKLIST 11 --- Keyboard Shortcut

### Shortcut wajib

-   [ ] Delete.
-   [ ] Arrow Up.
-   [ ] Arrow Down.
-   [ ] Arrow Left.
-   [ ] Arrow Right.
-   [ ] Shift + Arrow untuk perpindahan lebih besar.
-   [ ] Ctrl/Cmd + Z.
-   [ ] Ctrl/Cmd + Shift + Z.
-   [ ] Ctrl/Cmd + C.
-   [ ] Ctrl/Cmd + V.

### Aturan

-   [ ] Shortcut tidak bekerja saat user sedang mengetik di input.
-   [ ] Shortcut tidak mengganggu editor data resep.

### Lulus jika

-   [ ] Semua shortcut bekerja sesuai fungsi.
-   [ ] Input/textarea tetap dapat digunakan normal.

------------------------------------------------------------------------

## CHECKLIST 12 --- Undo / Redo

### Pekerjaan

Undo/redo harus mencakup: - \[ \] Edit data. - \[ \] Drag. - \[ \]
Resize. - \[ \] Rotation. - \[ \] Style. - \[ \] Image position. - \[ \]
Crop. - \[ \] Layer. - \[ \] Alignment. - \[ \] Page operation.

### Tidak masuk history

-   [ ] Klik selection.
-   [ ] Hover.
-   [ ] Membuka panel.
-   [ ] UI sementara.

### History grouping

-   [ ] Satu drag = satu action.
-   [ ] Satu resize = satu action.
-   [ ] Tidak membuat ratusan history entry dari satu gesture.

### Lulus jika

-   [ ] Undo mengembalikan kondisi sebelumnya.
-   [ ] Redo mengembalikan kondisi setelah undo.
-   [ ] Selection/hover tidak membuat history.

------------------------------------------------------------------------

## CHECKLIST 13 --- Zoom Canvas

### Pekerjaan

-   [ ] 50%.
-   [ ] 75%.
-   [ ] 100%.
-   [ ] Fit.

### Aturan

-   [ ] Zoom hanya mengubah tampilan editor.
-   [ ] Zoom tidak mengubah ukuran dokumen A4.

### Lulus jika

-   [ ] Ukuran A4 tetap 210mm × 297mm.
-   [ ] Export tidak terpengaruh zoom.

------------------------------------------------------------------------

## CHECKLIST 14 --- Page Settings

### Pekerjaan

-   [ ] A4.
-   [ ] Portrait.
-   [ ] Background halaman.

### Aturan

-   [ ] Tidak menambahkan ukuran kertas lain pada tahap ini.

### Lulus jika

-   [ ] Page settings konsisten dengan canvas dan export.

------------------------------------------------------------------------

# 3. EXPORT

## CHECKLIST 15 --- Export 1 Halaman

### Pekerjaan

Buat fungsi:

**Export Current Page**

### Hasil wajib

Jika halaman aktif adalah Page 1:

-   [ ] Output hanya Page 1.
-   [ ] Output = 1 halaman A4.

Tidak boleh ikut: - \[ \] Sidebar kiri. - \[ \] Editor kanan. - \[ \]
Toolbar. - \[ \] Canvas background. - \[ \] Selection outline. - \[ \]
Guide. - \[ \] Grid. - \[ \] UI editor.

### Lulus jika

-   [ ] Current Page menghasilkan tepat 1 halaman A4.
-   [ ] Halaman yang diekspor adalah halaman aktif.

------------------------------------------------------------------------

## CHECKLIST 16 --- Export Semua Halaman

### Pekerjaan

Buat fungsi:

**Export All Pages**

Jika editor memiliki:

-   Page 1
-   Page 2
-   Page 3

maka output harus:

-   [ ] PDF Page 1 = editor Page 1.
-   [ ] PDF Page 2 = editor Page 2.
-   [ ] PDF Page 3 = editor Page 3.

### Lulus jika

-   [ ] Jumlah halaman PDF = jumlah halaman editor.
-   [ ] Urutan PDF = urutan sidebar.
-   [ ] Tidak ada halaman kosong tambahan.

------------------------------------------------------------------------

# 4. KEWAJIBAN KESESUAIAN CANVAS DAN EXPORT

## CHECKLIST 17 --- Visual Match

Hasil export wajib mengikuti apa yang terlihat di canvas editor.

### Visual

-   [ ] Warna.
-   [ ] Background.
-   [ ] Gambar.
-   [ ] Crop.
-   [ ] Posisi.
-   [ ] Ukuran.
-   [ ] Bentuk.
-   [ ] Border.
-   [ ] Radius.
-   [ ] Shadow.
-   [ ] Opacity.
-   [ ] Rotation.

### Typography

-   [ ] Font.
-   [ ] Ukuran.
-   [ ] Weight.
-   [ ] Italic.
-   [ ] Line height.
-   [ ] Letter spacing.
-   [ ] Alignment.
-   [ ] Uppercase.

### Layout

-   [ ] X.
-   [ ] Y.
-   [ ] Width.
-   [ ] Height.
-   [ ] Layer order.

### Dokumen

-   [ ] A4.
-   [ ] Portrait.
-   [ ] Page order.

### Acceptance criteria

**Tidak boleh ada perbedaan visual yang berasal dari editor.**

------------------------------------------------------------------------

# 5. VERIFIKASI PDF

## CHECKLIST 18 --- PDF Verification

### Current Page

-   [ ] Pilih Page 1.
-   [ ] Export.
-   [ ] Pastikan hasil = 1 PDF page.
-   [ ] Pastikan hanya Page 1.

### Current Page lainnya

-   [ ] Pilih Page 2.
-   [ ] Export.
-   [ ] Pastikan hasil hanya Page 2.

### All Pages

-   [ ] Export semua.
-   [ ] Bandingkan jumlah halaman.
-   [ ] Bandingkan urutan halaman.

### Visual

Periksa setiap PDF page: - \[ \] Image. - \[ \] Warna. - \[ \] Text. -
\[ \] Posisi. - \[ \] Ukuran. - \[ \] Background. - \[ \] Border. - \[
\] Shadow. - \[ \] Crop.

------------------------------------------------------------------------

# 6. REGRESSION TEST

## CHECKLIST 19 --- Regression Test

-   [ ] Buka editor.
-   [ ] Klik canvas kosong.
-   [ ] Klik setiap element.
-   [ ] Drag element.
-   [ ] Resize element.
-   [ ] Edit text.
-   [ ] Edit style.
-   [ ] Upload image.
-   [ ] Crop image.
-   [ ] Zoom image.
-   [ ] Ubah layer.
-   [ ] Alignment.
-   [ ] Multi-select.
-   [ ] Undo.
-   [ ] Redo.
-   [ ] Duplicate page.
-   [ ] Add page.
-   [ ] Delete page.
-   [ ] Move page.
-   [ ] Export current page.
-   [ ] Export all pages.
-   [ ] Reload editor.
-   [ ] Pastikan tidak blank.
-   [ ] Pastikan tidak ada runtime error.

------------------------------------------------------------------------

# 7. DEFINITION OF DONE

## CHECKLIST 20 --- Pekerjaan Selesai

Pekerjaan hanya dianggap selesai jika semua item berikut lulus:

-   [ ] Canvas tidak blank.
-   [ ] Klik canvas tidak menyebabkan blank.
-   [ ] Semua element dapat dipilih.
-   [ ] Drag bekerja.
-   [ ] Resize bekerja.
-   [ ] Image tidak rusak.
-   [ ] Crop bekerja.
-   [ ] Layer bekerja.
-   [ ] Alignment bekerja.
-   [ ] Guides dan snap bekerja.
-   [ ] Multi-select bekerja.
-   [ ] Keyboard shortcut bekerja.
-   [ ] Undo bekerja.
-   [ ] Redo bekerja.
-   [ ] A4 tetap 210mm × 297mm.
-   [ ] Export current page menghasilkan tepat 1 halaman A4.
-   [ ] Export all pages menghasilkan jumlah halaman yang benar.
-   [ ] Tidak ada UI editor di PDF.
-   [ ] Warna PDF sama dengan canvas.
-   [ ] Gambar PDF sama dengan canvas.
-   [ ] Bentuk PDF sama dengan canvas.
-   [ ] Posisi PDF sama dengan canvas.
-   [ ] Ukuran PDF sama dengan canvas.
-   [ ] Font PDF sama dengan canvas.
-   [ ] Border PDF sama dengan canvas.
-   [ ] Shadow PDF sama dengan canvas.
-   [ ] Crop PDF sama dengan canvas.
-   [ ] Layer PDF sama dengan canvas.
-   [ ] Tidak ada halaman kosong tambahan.
-   [ ] Tidak ada runtime error.

------------------------------------------------------------------------

# 8. URUTAN YANG TIDAK BOLEH DIUBAH

1.  Stabilkan Struktur Editor
2.  Perbaiki A4
3.  Selection Element
4.  Drag Element
5.  Resize Element
6.  Image Editing
7.  Layer
8.  Alignment
9.  Guides dan Snap
10. Multi-Select
11. Keyboard Shortcut
12. Undo / Redo
13. Zoom Canvas
14. Page Settings
15. Export 1 Halaman
16. Export Semua Halaman
17. Visual Match Canvas dan Export
18. PDF Verification
19. Regression Test
20. Definition of Done

**Tidak boleh melompati tahap tanpa alasan teknis yang disetujui.**

**Tidak boleh mengerjakan pekerjaan di luar checklist.**

**Jika muncul kebutuhan baru di luar checklist, pekerjaan berhenti dan
menunggu persetujuan.**
