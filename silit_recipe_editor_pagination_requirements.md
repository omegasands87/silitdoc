# Dokumentasi Pagination Langkah Memasak

Status: DOKUMEN RESMI / TERKUNCI
Ruang lingkup: Recipe Editor — halaman Langkah Memasak
Repository kode: silit
Repository dokumentasi: silitdoc
Branch: main

## 1. Tujuan

Dokumen ini menetapkan perilaku resmi untuk menangani konten Langkah Memasak yang tidak lagi muat dalam satu halaman A4.

Tujuan:
- tidak ada konten yang terpotong karena batas halaman;
- keterbacaan tetap dipertahankan;
- langkah memasak dapat berlanjut ke halaman berikutnya secara otomatis;
- pengguna tidak perlu menghitung sendiri berapa langkah yang muat;
- setiap langkah diperlakukan sebagai satu unit konten yang utuh;
- Pro Tip dan footer tetap ditempatkan pada posisi yang dapat dibaca;
- hasil editor dan hasil export mengikuti pembagian halaman yang sama.

Dokumen ini dibuat sebagai dasar resmi pengerjaan dan verifikasi fitur pagination. Isi dokumen tidak boleh diubah selama pengerjaan, kecuali status checklist sesuai aturan dokumentasi proyek.

## 2. Masalah yang Ditemukan

Halaman Langkah Memasak saat ini menggunakan area halaman A4 dengan batas tetap. Ketika jumlah atau panjang langkah bertambah, konten terus ditempatkan ke halaman yang sama.

Akibatnya:
- langkah tambahan dapat keluar dari area halaman;
- Pro Tip dapat terdorong terlalu jauh ke bawah;
- footer dapat bertabrakan atau terpotong;
- sebagian konten dapat berada di luar area A4;
- pengguna tidak mendapatkan halaman lanjutan secara otomatis.

Contoh kasus: ketika Langkah Memasak memiliki 7 langkah, langkah tambahan dapat menyebabkan Pro Tip dan bagian bawah dokumen terpotong.

Masalah ini bukan alasan untuk mengecilkan seluruh isi secara paksa. Konten harus tetap terbaca.

## 3. Solusi Resmi

Solusi yang ditetapkan adalah automatic pagination.

Jika konten Langkah Memasak tidak lagi muat pada halaman aktif, sistem harus melanjutkan konten ke halaman berikutnya.

Contoh:

Halaman 03 — Langkah Memasak
- Langkah 1
- Langkah 2
- Langkah 3
- Langkah 4

Halaman 04 — Langkah Memasak (Lanjutan)
- Langkah 5
- Langkah 6
- Langkah 7
- Pro Tip
- Footer

Jumlah langkah per halaman tidak boleh ditetapkan sebagai angka tetap. Pembagian harus mengikuti ruang aktual yang tersedia dan ukuran konten.

## 4. Prinsip Pagination

### 4.1 Tidak memotong konten
Sistem tidak boleh membiarkan isi langkah, Pro Tip, atau footer terpotong oleh batas halaman.

### 4.2 Tidak mengecilkan isi secara paksa
Pagination tidak boleh diselesaikan dengan mengecilkan font, spacing, atau seluruh desain hanya agar semua konten masuk ke satu A4.

### 4.3 Satu langkah adalah satu unit
Satu langkah memasak sebaiknya tetap utuh pada satu halaman. Jika satu langkah tidak cukup ruang untuk ditampilkan secara utuh di sisa halaman, langkah tersebut dipindahkan ke halaman berikutnya selama hal itu memungkinkan.

### 4.4 Pembagian mengikuti ruang aktual
Sistem tidak boleh menggunakan aturan sederhana seperti “selalu 4 langkah per halaman”. Jumlah langkah yang muat dapat berbeda karena panjang judul dan deskripsi setiap langkah berbeda.

### 4.5 Pro Tip mengikuti konten
Pro Tip tidak boleh dipaksa tetap berada di halaman pertama jika langkah memasak membutuhkan ruang tersebut. Jika diperlukan, Pro Tip berpindah ke halaman berikutnya setelah blok langkah yang relevan.

### 4.6 Footer tetap terbaca
Footer harus tetap berada dalam area halaman dan tidak boleh tertutup atau terpotong oleh konten langkah.

## 5. Perilaku Editor

Pagination harus terlihat jelas di canvas editor.

Jika diperlukan halaman lanjutan:
- halaman lanjutan harus memiliki ukuran halaman yang sama;
- pembagian konten harus dapat dipahami pengguna;
- urutan langkah harus tetap benar;
- tidak boleh ada langkah yang hilang atau terduplikasi;
- nomor halaman harus mengikuti urutan dokumen;
- selection dan Layer harus tetap konsisten dengan halaman tempat konten berada.

Pagination tidak boleh membuat pengguna kehilangan konteks halaman atau object yang sedang diedit.

## 6. Perilaku Page dan Layer

Pagination tidak boleh menghilangkan struktur dokumen.

Jika satu konten Langkah Memasak menghasilkan beberapa halaman:
- halaman lanjutan harus dapat dikenali sebagai bagian dari Langkah Memasak;
- object yang berada pada halaman lanjutan harus tetap dapat dipilih;
- Layer harus menunjukkan object yang benar pada halaman aktif;
- selection dari canvas dan Layer harus mengarah ke inspector yang benar;
- KONTEN/DESAIN tetap mempertahankan state yang dipilih pengguna;
- KONTEN dengan mode Layer terpilih hanya menampilkan konten dari layer yang relevan.

## 7. Pro Tip dan Footer

Urutan akhir harus mengikuti struktur dokumen:
1. Langkah Memasak
2. Pro Tip
3. Footer

Jika seluruh langkah tidak muat dalam satu halaman, urutan tersebut tetap dipertahankan setelah pagination.

Contoh:

Halaman 03:
- Langkah 1
- Langkah 2
- Langkah 3
- Langkah 4

Halaman 04:
- Langkah 5
- Langkah 6
- Langkah 7
- Pro Tip
- Footer

Sistem tidak boleh menempatkan Pro Tip di tengah rangkaian langkah.

## 8. Kasus Satu Langkah Sangat Panjang

Jika satu langkah sangat panjang dan tidak muat pada satu halaman:
- sistem harus terlebih dahulu mencoba memindahkan seluruh langkah ke halaman berikutnya;
- langkah tidak boleh terpotong jika masih dapat dihindari;
- jika ukuran satu langkah secara individual memang melebihi satu halaman penuh, perilaku khusus harus ditentukan dan diverifikasi sebelum implementasi dianggap selesai.

Kasus terakhir tidak boleh diselesaikan dengan asumsi. Jika implementasi membutuhkan keputusan baru di luar aturan ini, pengerjaan harus berhenti dan keputusan tersebut harus didokumentasikan terlebih dahulu.

## 9. Export

Pagination pada editor dan export harus konsisten.

### Export Current
Jika halaman yang sedang dipilih merupakan bagian dari hasil pagination, export harus mengikuti halaman yang benar dan tidak menghasilkan konten terpotong.

### Export All
Seluruh halaman hasil pagination harus diexport dalam urutan yang benar.

Tidak boleh ada:
- halaman yang hilang;
- halaman duplikat;
- langkah yang hilang;
- urutan langkah yang berubah;
- Pro Tip atau footer yang terpotong.

## 10. Undo dan Redo

Perubahan yang memengaruhi pagination harus tetap kompatibel dengan Undo dan Redo.

Undo dan Redo tidak boleh menyebabkan:
- halaman lanjutan hilang secara tidak terduga;
- langkah berpindah ke urutan yang salah;
- selection menunjuk ke object yang tidak ada;
- halaman menjadi kosong tanpa alasan yang dapat dipahami.

## 11. Non-Goals

Dokumen ini tidak menetapkan:
- template desain halaman baru;
- sistem template visual baru;
- perubahan ukuran A4;
- perubahan orientasi halaman;
- perubahan fitur Page Settings;
- fitur editor baru yang tidak berhubungan dengan pagination;
- perubahan desain visual yang tidak diperlukan untuk pagination.

Pagination hanya menyelesaikan masalah overflow dan kesinambungan konten Langkah Memasak.

## 12. Acceptance Checklist

### A. Dasar Pagination
- [ ] Konten Langkah Memasak tidak terpotong ketika melebihi tinggi halaman.
- [ ] Sistem membuat kelanjutan halaman ketika ruang halaman tidak mencukupi.
- [ ] Tidak ada konten yang hilang saat pagination.
- [ ] Tidak ada konten yang terduplikasi saat pagination.
- [ ] Urutan langkah tetap benar.
- [ ] Tidak menggunakan jumlah langkah tetap sebagai batas halaman.

### B. Keterbacaan
- [ ] Font tidak diperkecil secara paksa untuk menghindari pagination.
- [ ] Spacing tidak dipaksa menjadi terlalu padat untuk menghindari pagination.
- [ ] Satu langkah tetap utuh pada satu halaman jika masih memungkinkan.
- [ ] Langkah yang tidak muat dipindahkan ke halaman berikutnya.
- [ ] Tidak ada clipping atau overlap akibat pagination.

### C. Pro Tip dan Footer
- [ ] Pro Tip tidak menutupi atau tertutup oleh langkah.
- [ ] Pro Tip mengikuti rangkaian langkah dan tidak muncul di tengah langkah.
- [ ] Pro Tip dapat berpindah ke halaman lanjutan jika diperlukan.
- [ ] Footer tetap berada dalam area halaman.
- [ ] Footer tidak terpotong.
- [ ] Urutan Langkah → Pro Tip → Footer tetap konsisten.

### D. Page dan Layer
- [ ] Halaman lanjutan memiliki ukuran halaman yang konsisten.
- [ ] Halaman lanjutan dapat dikenali sebagai bagian dari Langkah Memasak.
- [ ] Object pada halaman lanjutan dapat dipilih.
- [ ] Layer menampilkan object dari halaman aktif dengan benar.
- [ ] Selection canvas dan Layer tetap konsisten.
- [ ] Inspector mengikuti object yang dipilih.
- [ ] KONTEN/DESAIN tidak berpindah secara tidak sengaja.
- [ ] Mode Layer terpilih pada KONTEN hanya menampilkan konten layer yang relevan.

### E. Export
- [ ] Export Current menghasilkan halaman yang benar tanpa clipping.
- [ ] Export All menghasilkan seluruh halaman pagination.
- [ ] Urutan halaman export benar.
- [ ] Tidak ada halaman yang hilang atau terduplikasi.
- [ ] Seluruh langkah tetap ada pada export.
- [ ] Pro Tip dan footer tetap terbaca pada export.

### F. Undo dan Redo
- [ ] Undo tetap bekerja setelah perubahan yang memengaruhi pagination.
- [ ] Redo tetap bekerja setelah perubahan yang memengaruhi pagination.
- [ ] Undo/Redo tidak membuat halaman lanjutan rusak.
- [ ] Undo/Redo tidak membuat selection menunjuk ke object yang tidak ada.

### G. Regression
- [ ] Cover tetap bekerja.
- [ ] Isi tetap bekerja.
- [ ] Langkah Memasak tetap dapat diedit.
- [ ] Tambah langkah tetap bekerja.
- [ ] Hapus langkah tetap bekerja.
- [ ] Edit judul langkah tetap bekerja.
- [ ] Edit deskripsi langkah tetap bekerja.
- [ ] Pro Tip tetap dapat diedit.
- [ ] Footer tetap dapat diedit.
- [ ] Page selection tetap bekerja.
- [ ] Layer selection tetap bekerja.
- [ ] Reload tidak menghasilkan halaman kosong.
- [ ] Tidak ada runtime error selama pengujian.

## 13. Aturan Verifikasi

Checklist hanya boleh diubah dari [ ] menjadi [x] setelah item benar-benar selesai dan diverifikasi.

Perubahan kode saja tidak cukup untuk mencentang item yang membutuhkan verifikasi visual atau runtime.

Jika informasi atau perilaku yang dibutuhkan tidak cukup jelas, jangan membuat asumsi. Hentikan bagian tersebut dan dokumentasikan kebutuhan keputusan baru sebelum melanjutkan.

## 14. Aturan Scope

Pengerjaan pagination hanya boleh menyentuh kebutuhan yang tercantum dalam dokumen ini.

Jika ditemukan kebutuhan baru di luar dokumen:
1. hentikan pengerjaan bagian tersebut;
2. jelaskan masalahnya;
3. jelaskan dampaknya terhadap scope;
4. usulkan perubahan dokumentasi;
5. tunggu persetujuan sebelum coding.

Dokumen ini menjadi acuan resmi untuk implementasi dan verifikasi pagination Langkah Memasak.
