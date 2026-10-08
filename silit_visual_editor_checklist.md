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

-   <span style="color:green">✅</span> Pertahankan ukuran A4: 210mm × 297mm.
-   <span style="color:green">✅</span> Canvas tetap portrait.
-   <span style="color:green">✅</span> Canvas memiliki background.
-   <span style="color:green">✅</span> Overflow canvas terkendali.
-   <span style="color:green">✅</span> Cover image kembali memiliki area 60% A4.
-   <span style="color:green">✅</span> Area informasi cover tetap 40% A4.

### Hasil wajib

-   Proporsi cover sama dengan desain awal.
-   Selection editor tidak mengubah ukuran image.
-   Selection editor tidak mengubah pembagian 60% / 40%.

### Lulus jika

-   <span style="color:green">✅</span> Cover image tidak mengecil karena wrapper editor.
-   <span style="color:green">✅</span> Canvas tidak blank.

------------------------------------------------------------------------

## CHECKLIST 03 --- Selection Element

### Element Cover

-   <span style="color:green">✅</span> Foto Sampul
-   <span style="color:green">✅</span> Kategori
-   <span style="color:green">✅</span> Judul
-   <span style="color:green">✅</span> Kutipan
-   <span style="color:green">✅</span> Meta

### Element Isi

-   <span style="color:green">✅</span> Judul Cerita
-   <span style="color:green">✅</span> Teks Cerita
-   <span style="color:green">✅</span> Bahan
-   <span style="color:green">✅</span> Alat
-   <span style="color:green">✅</span> Nutrisi
-   <span style="color:green">✅</span> Footer

### Element Cooking

-   <span style="color:green">✅</span> Judul Memasak
-   <span style="color:green">✅</span> Langkah
-   <span style="color:green">✅</span> Pro Tip
-   <span style="color:green">✅</span> Footer

### Interaction

-   <span style="color:green">✅</span> Klik element memilih element.
-   <span style="color:green">✅</span> Bounding box muncul.
-   <span style="color:green">✅</span> Panel kanan menampilkan element yang dipilih.
-   <span style="color:green">✅</span> Klik area kosong menghapus selection.
-   <span style="color:green">✅</span> Klik area kosong tidak menyebabkan blank.

### Lulus jika

-   <span style="color:green">✅</span> Semua element pada daftar dapat dipilih.
-   <span style="color:green">✅</span> Selection tidak merusak layout.

------------------------------------------------------------------------

## CHECKLIST 04 --- Drag Element

### Pekerjaan

-   <span style="color:green">✅</span> Element dapat di-drag langsung di canvas.
-   <span style="color:green">✅</span> Posisi mengikuti mouse.
-   <span style="color:green">✅</span> Posisi X/Y diperbarui.
-   <span style="color:green">✅</span> Perubahan X/Y dari panel mengubah posisi element.
-   <span style="color:green">✅</span> Canvas tetap stabil setelah drag.

### Lulus jika

-   <span style="color:green">✅</span> Posisi canvas dan panel X/Y konsisten.
-   <span style="color:green">✅</span> Element lain tidak ikut berpindah.

------------------------------------------------------------------------

## CHECKLIST 05 --- Resize Element

### Pekerjaan

-   <span style="color:green">✅</span> Tambahkan handle kiri.
-   <span style="color:green">✅</span> Tambahkan handle kanan.
-   <span style="color:green">✅</span> Tambahkan handle atas.
-   <span style="color:green">✅</span> Tambahkan handle bawah.
-   <span style="color:green">✅</span> Tambahkan 4 corner handle.
-   <span style="color:green">✅</span> Resize memperbarui width/height.
-   <span style="color:green">✅</span> Resize tidak merusak element lain.
-   <span style="color:green">✅</span> Resize tidak menyebabkan blank.

### Image

-   <span style="color:green">✅</span> Frame image tetap valid.
-   <span style="color:green">✅</span> Image tetap berada di dalam frame.

### Lulus jika

-   <span style="color:green">✅</span> Resize dari canvas dan ukuran pada model konsisten.

------------------------------------------------------------------------

## CHECKLIST 06 --- Image Editing

### Pekerjaan

-   <span style="color:green">✅</span> Replace image.
-   <span style="color:green">✅</span> Crop image.
-   <span style="color:green">✅</span> Position image di dalam frame.
-   <span style="color:green">✅</span> Zoom image di dalam frame.
-   <span style="color:green">✅</span> Fit: Cover.
-   <span style="color:green">✅</span> Fit: Contain.

### Lulus jika

-   <span style="color:green">✅</span> Frame tidak berubah saat image digeser.
-   <span style="color:green">✅</span> Crop terlihat benar di canvas.
-   <span style="color:green">✅</span> Zoom terlihat benar di canvas.
-   <span style="color:green">✅</span> Position terlihat benar di canvas.
-   <span style="color:green">✅</span> Hasil export mengikuti crop, zoom, dan position canvas.

------------------------------------------------------------------------

## CHECKLIST 07 --- Layer

### Pekerjaan

-   <span style="color:green">✅</span> Bring Forward.
-   <span style="color:green">✅</span> Send Backward.
-   <span style="color:green">✅</span> Bring to Front.
-   <span style="color:green">✅</span> Send to Back.
-   <span style="color:green">✅</span> Tampilkan layer element halaman aktif.
-   <span style="color:green">✅</span> Urutan layer panel sama dengan hasil visual canvas.

### Lulus jika

-   <span style="color:green">✅</span> Perubahan layer langsung terlihat di canvas.
-   <span style="color:green">✅</span> Urutan layer tidak berubah saat export.

------------------------------------------------------------------------

## CHECKLIST 08 --- Alignment

### Pekerjaan

-   <span style="color:green">✅</span> Align Left.
-   <span style="color:green">✅</span> Align Center.
-   <span style="color:green">✅</span> Align Right.
-   <span style="color:green">✅</span> Align Top.
-   <span style="color:green">✅</span> Align Middle.
-   <span style="color:green">✅</span> Align Bottom.
-   <span style="color:green">✅</span> Center Horizontally.
-   <span style="color:green">✅</span> Center Vertically.

### Lulus jika

-   <span style="color:green">✅</span> Element berpindah sesuai perintah alignment.
-   <span style="color:green">✅</span> Posisi hasil alignment konsisten dengan canvas.

------------------------------------------------------------------------

## CHECKLIST 09 --- Guides dan Snap

### Pekerjaan

-   <span style="color:green">✅</span> Center guide.
-   <span style="color:green">✅</span> Edge alignment guide.
-   <span style="color:green">✅</span> Snap ke guide.
-   <span style="color:green">✅</span> Snap ke element lain.

### Hasil wajib

-   Guide muncul saat diperlukan.
-   Element dapat disejajarkan dengan mudah.

### Lulus jika

-   <span style="color:green">✅</span> Snap tidak memindahkan element secara tidak terduga.
-   <span style="color:green">✅</span> Guide tidak ikut muncul pada hasil export.

------------------------------------------------------------------------

## CHECKLIST 10 --- Multi-Select

### Pekerjaan

-   <span style="color:green">✅</span> Pilih element pertama.
-   <span style="color:green">✅</span> Tambahkan element menggunakan modifier key.
-   <span style="color:green">✅</span> Semua element yang dipilih terlihat.
-   <span style="color:green">✅</span> Alignment dapat digunakan untuk selection.

### Lulus jika

-   <span style="color:green">✅</span> Multi-select tidak merusak layout.
-   <span style="color:green">✅</span> Element yang tidak dipilih tidak ikut berubah.

------------------------------------------------------------------------

## CHECKLIST 11 --- Keyboard Shortcut

### Shortcut wajib

-   <span style="color:green">✅</span> Delete.
-   <span style="color:green">✅</span> Arrow Up.
-   <span style="color:green">✅</span> Arrow Down.
-   <span style="color:green">✅</span> Arrow Left.
-   <span style="color:green">✅</span> Arrow Right.
-   <span style="color:green">✅</span> Shift + Arrow untuk perpindahan lebih besar.
-   <span style="color:green">✅</span> Ctrl/Cmd + Z.
-   <span style="color:green">✅</span> Ctrl/Cmd + Shift + Z.
-   <span style="color:green">✅</span> Ctrl/Cmd + C.
-   <span style="color:green">✅</span> Ctrl/Cmd + V.

### Aturan

-   <span style="color:green">✅</span> Shortcut tidak bekerja saat user sedang mengetik di input.
-   <span style="color:green">✅</span> Shortcut tidak mengganggu editor data resep.

### Lulus jika

-   <span style="color:green">✅</span> Semua shortcut bekerja sesuai fungsi.
-   <span style="color:green">✅</span> Input/textarea tetap dapat digunakan normal.

------------------------------------------------------------------------

## CHECKLIST 12 --- Undo / Redo

### Pekerjaan

Undo/redo harus mencakup: - \[ \] Edit data. - \[ \] Drag. - \[ \]
Resize. - \[ \] Rotation. - \[ \] Style. - \[ \] Image position. - \[ \]
Crop. - \[ \] Layer. - \[ \] Alignment. - \[ \] Page operation.

### Tidak masuk history

-   <span style="color:green">✅</span> Klik selection.
-   <span style="color:green">✅</span> Hover.
-   <span style="color:green">✅</span> Membuka panel.
-   <span style="color:green">✅</span> UI sementara.

### History grouping

-   <span style="color:green">✅</span> Satu drag = satu action.
-   <span style="color:green">✅</span> Satu resize = satu action.
-   <span style="color:green">✅</span> Tidak membuat ratusan history entry dari satu gesture.

### Lulus jika

-   <span style="color:green">✅</span> Undo mengembalikan kondisi sebelumnya.
-   <span style="color:green">✅</span> Redo mengembalikan kondisi setelah undo.
-   <span style="color:green">✅</span> Selection/hover tidak membuat history.

------------------------------------------------------------------------

## CHECKLIST 13 --- Zoom Canvas

### Pekerjaan

-   <span style="color:green">✅</span> 50%.
-   <span style="color:green">✅</span> 75%.
-   <span style="color:green">✅</span> 100%.
-   <span style="color:green">✅</span> Fit.

### Aturan

-   <span style="color:green">✅</span> Zoom hanya mengubah tampilan editor.
-   <span style="color:green">✅</span> Zoom tidak mengubah ukuran dokumen A4.

### Lulus jika

-   <span style="color:green">✅</span> Ukuran A4 tetap 210mm × 297mm.
-   <span style="color:green">✅</span> Export tidak terpengaruh zoom.

------------------------------------------------------------------------

## CHECKLIST 14 --- Page Settings

### Pekerjaan

-   <span style="color:green">✅</span> A4.
-   <span style="color:green">✅</span> Portrait.
-   <span style="color:green">✅</span> Background halaman.

### Aturan

-   <span style="color:green">✅</span> Tidak menambahkan ukuran kertas lain pada tahap ini.

### Lulus jika

-   <span style="color:green">✅</span> Page settings konsisten dengan canvas dan export.

------------------------------------------------------------------------

# 3. EXPORT

## CHECKLIST 15 --- Export 1 Halaman

### Pekerjaan

Buat fungsi:

**Export Current Page**

### Hasil wajib

Jika halaman aktif adalah Page 1:

-   <span style="color:green">✅</span> Output hanya Page 1.
-   <span style="color:green">✅</span> Output = 1 halaman A4.

Tidak boleh ikut: - \[ \] Sidebar kiri. - \[ \] Editor kanan. - \[ \]
Toolbar. - \[ \] Canvas background. - \[ \] Selection outline. - \[ \]
Guide. - \[ \] Grid. - \[ \] UI editor.

### Lulus jika

-   <span style="color:green">✅</span> Current Page menghasilkan tepat 1 halaman A4.
-   <span style="color:green">✅</span> Halaman yang diekspor adalah halaman aktif.

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

-   <span style="color:green">✅</span> PDF Page 1 = editor Page 1.
-   <span style="color:green">✅</span> PDF Page 2 = editor Page 2.
-   <span style="color:green">✅</span> PDF Page 3 = editor Page 3.

### Lulus jika

-   <span style="color:green">✅</span> Jumlah halaman PDF = jumlah halaman editor.
-   <span style="color:green">✅</span> Urutan PDF = urutan sidebar.
-   <span style="color:green">✅</span> Tidak ada halaman kosong tambahan.

------------------------------------------------------------------------

# 4. KEWAJIBAN KESESUAIAN CANVAS DAN EXPORT

## CHECKLIST 17 --- Visual Match

Hasil export wajib mengikuti apa yang terlihat di canvas editor.

### Visual

-   <span style="color:green">✅</span> Warna.
-   <span style="color:green">✅</span> Background.
-   <span style="color:green">✅</span> Gambar.
-   <span style="color:green">✅</span> Crop.
-   <span style="color:green">✅</span> Posisi.
-   <span style="color:green">✅</span> Ukuran.
-   <span style="color:green">✅</span> Bentuk.
-   <span style="color:green">✅</span> Border.
-   <span style="color:green">✅</span> Radius.
-   <span style="color:green">✅</span> Shadow.
-   <span style="color:green">✅</span> Opacity.
-   <span style="color:green">✅</span> Rotation.

### Typography

-   <span style="color:green">✅</span> Font.
-   <span style="color:green">✅</span> Ukuran.
-   <span style="color:green">✅</span> Weight.
-   <span style="color:green">✅</span> Italic.
-   <span style="color:green">✅</span> Line height.
-   <span style="color:green">✅</span> Letter spacing.
-   <span style="color:green">✅</span> Alignment.
-   <span style="color:green">✅</span> Uppercase.

### Layout

-   <span style="color:green">✅</span> X.
-   <span style="color:green">✅</span> Y.
-   <span style="color:green">✅</span> Width.
-   <span style="color:green">✅</span> Height.
-   <span style="color:green">✅</span> Layer order.

### Dokumen

-   <span style="color:green">✅</span> A4.
-   <span style="color:green">✅</span> Portrait.
-   <span style="color:green">✅</span> Page order.

### Acceptance criteria

**Tidak boleh ada perbedaan visual yang berasal dari editor.**

------------------------------------------------------------------------

# 5. VERIFIKASI PDF

## CHECKLIST 18 --- PDF Verification

### Current Page

-   <span style="color:green">✅</span> Pilih Page 1.
-   <span style="color:green">✅</span> Export.
-   <span style="color:green">✅</span> Pastikan hasil = 1 PDF page.
-   <span style="color:green">✅</span> Pastikan hanya Page 1.

### Current Page lainnya

-   <span style="color:green">✅</span> Pilih Page 2.
-   <span style="color:green">✅</span> Export.
-   <span style="color:green">✅</span> Pastikan hasil hanya Page 2.

### All Pages

-   <span style="color:green">✅</span> Export semua.
-   <span style="color:green">✅</span> Bandingkan jumlah halaman.
-   <span style="color:green">✅</span> Bandingkan urutan halaman.

### Visual

Periksa setiap PDF page: - <span style="color:green">✅</span> Image. - <span style="color:green">✅</span> Warna. - <span style="color:green">✅</span> Text. -
<span style="color:green">✅</span> Posisi. - <span style="color:green">✅</span> Ukuran. - <span style="color:green">✅</span> Background. - <span style="color:green">✅</span> Border. - <span style="color:green">✅</span> Shadow. - <span style="color:green">✅</span> Crop.

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
