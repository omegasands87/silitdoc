# SILIT — Dokumentasi Khusus Perbaikan Hasil Audit UI/UX Editor

## Status Dokumen

- Dokumen ini adalah spesifikasi tetap untuk pekerjaan perbaikan hasil audit UI/UX halaman editor.
- Setelah file ini dibuat, isi dokumen **tidak boleh diubah**.
- Perubahan setelah pembuatan dokumen **hanya boleh berupa status centang checklist pekerjaan**.
- Tidak boleh menambah, menghapus, memindahkan, atau menulis ulang isi checklist.
- Tidak boleh mengubah urutan, nomor, judul, requirement, batasan, atau kriteria penerimaan.
- Pekerjaan kode tetap dilakukan hanya pada repository `silit`.
- Dokumentasi ini berada di repository `silitdoc`.
- Semua perubahan kode langsung ke branch `main`.
- Tidak boleh membuat branch lain.
- AI tidak boleh melakukan deployment dalam bentuk apa pun.

---

## 1. Tujuan Perbaikan

Memperbaiki struktur informasi, hierarki, dan alur penggunaan sidebar halaman editor agar mental model pengguna jelas:

`PAGE → LAYER → SELECTED OBJECT → DESIGN PROPERTIES`

Saat tidak ada object yang dipilih:

`PAGE → DESIGN → PAGE/CANVAS PROPERTIES`

Perbaikan harus mengatasi masalah yang ditemukan pada audit UI/UX, bukan sekadar mengganti warna, border, spacing, atau kosmetik.

---

## 2. Masalah Audit yang Menjadi Dasar Perbaikan

### 2.1 Struktur Page dan Layer terlalu eksklusif

- Page dan Layer berada pada tab yang saling menyembunyikan.
- Saat Page aktif, konteks Layer hilang.
- Saat Layer aktif, konteks Page hilang.
- Kondisi ini meningkatkan context switching dan kebutuhan mengingat posisi informasi.

### 2.2 Konten dan Desain salah klasifikasi

- Page Settings dan pengaturan layout berada di area Konten.
- Pengaturan halaman/canvas bukan konten objek.
- Informasi tersebut harus mengikuti mental model pengaturan desain/halaman.

### 2.3 Desain kosong ketika tidak ada object terpilih

- Panel Desain dapat berakhir pada kondisi tidak ada elemen dipilih.
- Panel tidak memberikan konteks desain halaman/canvas ketika tidak ada selection.
- Kondisi kosong harus tetap memiliki fungsi yang relevan.

### 2.4 Inspector belum cukup kontekstual

- Selection context sudah ada tetapi struktur panel masih terasa seperti form umum.
- Inspector harus mengikuti object yang sedang dipilih.
- Jenis object harus menentukan properti yang relevan.

### 2.5 Layer terlalu teknis

- Nilai seperti z-index menjadi informasi utama.
- Singkatan seperti IMG/TXT/GRP terlalu teknis.
- Nama layer seperti nama variable internal kurang berorientasi pengguna.

### 2.6 Inspector terlalu panjang dan datar

- Banyak section tampil sekaligus.
- Banyak card dan border membuat panel terasa padat.
- Hierarki visual belum cukup kuat untuk membedakan prioritas properti.

### 2.7 Konteks dokumen dan object belum cukup jelas

- Header panel masih terlalu berorientasi dokumen ketika object sedang dipilih.
- Ketika selection aktif, pengguna perlu mengetahui object yang sedang diedit.

### 2.8 Hierarki sidebar kiri belum konsisten

- Navigasi halaman, struktur layer, history, dan page actions terasa seperti beberapa sistem yang ditempel menjadi satu.
- Struktur utama harus mudah dipahami sebelum pengguna masuk ke action sekunder.

---

## 3. Prinsip Desain yang Wajib Dipertahankan

### 3.1 Visibility of system status

- Status halaman aktif harus jelas.
- Status object terpilih harus jelas.
- Status panel aktif harus jelas.
- Perubahan selection harus terlihat tanpa pengguna harus mengingat state sebelumnya.

### 3.2 Match between system and real world

- Gunakan istilah yang dipahami pengguna editor visual.
- Hindari menjadikan istilah implementasi sebagai informasi utama.
- Layer harus dipahami sebagai struktur visual, bukan daftar variable internal.

### 3.3 User control and freedom

- Pengguna harus dapat berpindah Page, Layer, Konten, dan Desain tanpa kehilangan konteks yang tidak perlu.
- Action layer order harus mudah ditemukan.
- State selection tidak boleh membuat pengguna kehilangan jalan kembali ke konteks halaman.

### 3.4 Consistency and standards

- Struktur sidebar harus mengikuti pola editor visual profesional.
- Page/Layer berada pada area navigasi/struktur.
- Properti object berada pada inspector.
- Properti harus berubah secara kontekstual sesuai selection.

### 3.5 Recognition rather than recall

- Informasi penting harus terlihat.
- Jangan memaksa pengguna mengingat tab sebelumnya untuk menemukan konteks.
- Nama, icon, status, dan hierarchy harus membantu pengenalan.

### 3.6 Aesthetic and minimalist design

- Kurangi nested card yang tidak diperlukan.
- Kurangi border yang tidak memberi fungsi.
- Kurangi label kecil yang berlebihan.
- Pertahankan whitespace yang cukup.
- Prioritaskan informasi dan action yang paling sering digunakan.

### 3.7 Error prevention

- Struktur panel harus mencegah pengguna salah memahami apakah sedang mengedit halaman atau object.
- Action yang tidak relevan dengan selection tidak boleh menjadi fokus utama.

### 3.8 Flexibility and efficiency

- Selection dari canvas dan layer harus membawa pengguna ke konteks property yang benar.
- Pengguna berpengalaman harus dapat melakukan action utama tanpa navigasi berulang yang tidak perlu.

---

## 4. Target Arsitektur UI

### 4.1 Sidebar kiri

Sidebar kiri menjadi area struktur dokumen:

- PAGE
- LAYER

Keduanya harus diperlakukan sebagai konteks utama struktur editor.

### 4.2 Sidebar kanan

Sidebar kanan menjadi inspector:

- KONTEN
- DESAIN

Sidebar kanan tidak menjadi tempat utama struktur layer.

### 4.3 Saat tidak ada selection

Panel kanan harus tetap berguna untuk konteks halaman/canvas.

### 4.4 Saat ada selection

Panel kanan harus berubah menjadi inspector object yang dipilih.

### 4.5 Layer

Panel Layer harus berfokus pada:

- nama layer
- icon/type yang mudah dikenali
- urutan layer
- selection state
- action pengaturan urutan

Detail implementasi seperti z-index tidak boleh menjadi informasi visual utama jika tidak dibutuhkan pengguna.

---

# 5. Checklist Pekerjaan Perbaikan

## A. Audit Baseline

- [ ] Verifikasi struktur sidebar kiri saat kondisi Page.
- [ ] Verifikasi struktur sidebar kiri saat kondisi Layer.
- [ ] Verifikasi struktur sidebar kanan saat tidak ada selection.
- [ ] Verifikasi struktur sidebar kanan saat object dipilih.
- [ ] Verifikasi hubungan selection canvas dengan inspector.
- [ ] Verifikasi hubungan selection layer dengan inspector.
- [ ] Verifikasi hierarchy Page → Layer → Object → Properties.
- [ ] Catat hanya masalah yang termasuk scope dokumentasi ini.

## B. Struktur Sidebar Kiri

- [ ] Page dan Layer memiliki struktur navigasi yang jelas.
- [ ] Pengguna dapat berpindah Page tanpa kehilangan pemahaman struktur dokumen.
- [ ] Pengguna dapat membuka Layer tanpa kehilangan konteks halaman aktif.
- [ ] Page navigation tidak bercampur dengan inspector object.
- [ ] History dan Page Actions tidak mengambil prioritas visual dari struktur utama.
- [ ] Active state Page jelas tetapi tidak berlebihan.
- [ ] Active state Layer jelas tetapi tidak berlebihan.

## C. Panel Layer

- [ ] Layer list memiliki hierarchy visual yang jelas.
- [ ] Layer row memiliki nama yang mudah dikenali.
- [ ] Layer row memiliki icon/type yang mudah dikenali.
- [ ] Selection layer terlihat jelas.
- [ ] Urutan layer mudah dipahami.
- [ ] Action Paling depan tersedia.
- [ ] Action Naik tersedia.
- [ ] Action Turun tersedia.
- [ ] Action Paling belakang tersedia.
- [ ] Informasi teknis tidak menjadi fokus utama.
- [ ] Nama layer tidak terasa seperti nama variable internal jika dapat diperbaiki tanpa mengubah data yang tidak diminta.
- [ ] Layer panel tidak menjadi form panjang.

## D. Struktur Sidebar Kanan

- [ ] Sidebar kanan hanya berfungsi sebagai inspector Konten dan Desain.
- [ ] Konten berisi kontrol yang benar-benar berkaitan dengan konten.
- [ ] Page/canvas properties tidak salah diklasifikasikan sebagai object content.
- [ ] Desain berisi property desain yang relevan dengan context.
- [ ] Struktur panel tidak menampilkan Layer sebagai tab kanan.
- [ ] Hierarchy tab Konten/Desain jelas.
- [ ] Active tab terlihat jelas tanpa visual berlebihan.

## E. Contextual Inspector

- [ ] Saat tidak ada object dipilih, panel Desain tetap memiliki fungsi yang relevan.
- [ ] Saat object dipilih, panel Desain menunjukkan context object tersebut.
- [ ] Nama object yang dipilih terlihat jelas.
- [ ] Type object terlihat dengan bahasa yang mudah dipahami.
- [ ] Properti yang tampil mengikuti type object.
- [ ] Properti yang tidak relevan tidak mengambil ruang utama.
- [ ] Selection dari canvas membuka context inspector yang benar.
- [ ] Selection dari Layer membuka context inspector yang benar.
- [ ] Clearing selection mengembalikan context halaman/canvas dengan benar.

## F. Hierarchy dan Information Density

- [ ] Section utama dapat dibedakan dalam sekali scan.
- [ ] Section sekunder tidak mengalahkan action utama.
- [ ] Nested card yang tidak diperlukan dikurangi.
- [ ] Border hanya digunakan jika memberi fungsi.
- [ ] Label uppercase tidak digunakan secara berlebihan.
- [ ] Spacing antar kelompok property konsisten.
- [ ] Panel tidak terasa seperti form panjang tanpa hierarchy.
- [ ] Informasi penting berada pada posisi yang mudah ditemukan.

## G. Konsistensi Interaction

- [ ] Selection state konsisten antara canvas, layer, dan inspector.
- [ ] Active page konsisten antara canvas dan Page panel.
- [ ] Layer order konsisten antara visual canvas dan Layer panel.
- [ ] Action layer order menghasilkan perubahan yang terlihat dan dapat dipahami.
- [ ] Navigasi antar panel tidak mengubah data secara tidak sengaja.
- [ ] Tidak ada state panel yang membuat pengguna kehilangan konteks.

## H. Error Prevention dan Recovery

- [ ] Pengguna tidak mudah salah memahami apakah sedang mengedit Page atau Object.
- [ ] Control yang tidak relevan tidak tampil sebagai action utama.
- [ ] Tidak ada action yang menghilang tanpa alasan yang dapat dipahami.
- [ ] State kosong memiliki pesan atau control yang membantu.
- [ ] Perubahan UI tidak merusak state editor yang sudah ada.
- [ ] Perubahan UI tidak mengubah fitur editor di luar scope.

## I. Visual QA

- [ ] Sidebar kiri memiliki hierarchy visual yang jelas.
- [ ] Sidebar kanan memiliki hierarchy visual yang jelas.
- [ ] Canvas tetap menjadi area kerja utama.
- [ ] Sidebar tidak mengambil perhatian lebih besar dari canvas tanpa alasan.
- [ ] Typography panel konsisten.
- [ ] Iconography konsisten.
- [ ] Spacing konsisten.
- [ ] Active state konsisten.
- [ ] Selected state konsisten.
- [ ] Tidak ada clipping.
- [ ] Tidak ada overflow yang mengganggu.
- [ ] Tidak ada elemen yang saling menimpa.

## J. Regression UI/UX

- [ ] Page selection tetap berfungsi.
- [ ] Layer selection tetap berfungsi.
- [ ] Element selection tetap berfungsi.
- [ ] Drag tetap berfungsi.
- [ ] Resize tetap berfungsi.
- [ ] Edit text tetap berfungsi.
- [ ] Edit style tetap berfungsi.
- [ ] Upload image tetap berfungsi.
- [ ] Crop image tetap berfungsi.
- [ ] Zoom image tetap berfungsi.
- [ ] Layer ordering tetap berfungsi.
- [ ] Alignment tetap berfungsi.
- [ ] Multi-select tetap berfungsi.
- [ ] Undo tetap berfungsi.
- [ ] Redo tetap berfungsi.
- [ ] Add page tetap berfungsi.
- [ ] Duplicate page tetap berfungsi.
- [ ] Delete page tetap berfungsi.
- [ ] Move page tetap berfungsi.
- [ ] Export current page tetap berfungsi.
- [ ] Export all pages tetap berfungsi.
- [ ] Reload editor tidak menghasilkan blank state.
- [ ] Tidak ada runtime error yang muncul dari perubahan ini.

## K. Scope Control

- [x] Hanya area UI/UX editor yang termasuk dokumentasi ini yang diubah.
- [x] Tidak mengubah toolbar/canvas/export/fitur lain yang tidak diperlukan oleh audit ini.
- [x] Tidak menambah fitur di luar kebutuhan audit.
- [x] Tidak mengubah checklist lama kecuali update centang pekerjaan yang memang telah diverifikasi.
- [x] Tidak mengubah isi dokumentasi ini.
- [x] Tidak membuat branch baru.
- [x] Semua perubahan kode langsung ke `main`.
- [x] Tidak melakukan deployment.
- [x] Tidak mengklaim pekerjaan selesai tanpa verifikasi.

## L. Acceptance Criteria

- [ ] Mental model PAGE → LAYER → SELECTED OBJECT → DESIGN PROPERTIES terasa jelas.
- [ ] Kondisi tanpa selection tetap memiliki konteks yang berguna.
- [ ] Page dan Layer mudah ditemukan.
- [ ] Konten dan Desain memiliki batas fungsi yang jelas.
- [ ] Inspector terasa kontekstual, bukan form generik.
- [ ] Layer terasa sebagai struktur visual, bukan daftar detail teknis.
- [ ] Hierarchy informasi dapat dipahami tanpa mengingat state sebelumnya.
- [ ] UI lebih ringan secara visual tanpa kehilangan fungsi.
- [ ] Interaction utama dapat ditemukan tanpa context switching yang tidak perlu.
- [ ] Seluruh regression UI/UX yang termasuk scope telah diverifikasi.
- [ ] Tidak ada perubahan di luar scope.
- [ ] Tidak ada deployment yang dilakukan oleh AI.

---

## 6. Aturan Mutlak Setelah Dokumen Dibuat

1. Isi dokumen ini tidak boleh ditulis ulang.
2. Isi dokumen ini tidak boleh diringkas lalu menggantikan versi asli.
3. Judul, urutan, nomor, requirement, prinsip, target arsitektur, checklist, dan acceptance criteria tidak boleh diubah.
4. Hanya status checkbox pekerjaan yang boleh diperbarui setelah pekerjaan diverifikasi.
5. Checkbox hanya boleh dicentang jika pekerjaan benar-benar telah selesai dan diverifikasi.
6. Tidak boleh mencentang pekerjaan berdasarkan asumsi.
7. Tidak boleh mencentang pekerjaan berdasarkan niat, rencana, atau perubahan kode yang belum diverifikasi.
8. Jika ada kebutuhan baru di luar dokumen ini, hentikan pekerjaan dan minta persetujuan sebelum mengubah scope.
9. Repository `silitdoc` hanya untuk dokumentasi dan checklist.
10. Repository `silit` hanya untuk pekerjaan kode.
11. Branch yang digunakan hanya `main`.
12. Deployment tetap menjadi hak owner dan tidak boleh dilakukan oleh AI.
