# SILIT — Catatan Pekerjaan yang Telah Dikerjakan

Status: DOKUMENTASI STATUS PEKERJAAN
Repository kode: silit
Repository dokumentasi: silitdoc
Branch: main

## Catatan Penting

Dokumen ini mencatat perubahan yang sudah dikerjakan pada Recipe Editor.

Dokumen ini **bukan checklist verifikasi**.

Item di bawah menjelaskan pekerjaan yang telah diimplementasikan atau diperbaiki. Pekerjaan yang membutuhkan verifikasi browser/runtime tidak dinyatakan terverifikasi hanya berdasarkan perubahan kode.

## 1. Perbaikan Struktur UI/UX Editor

### Sidebar kiri
- Page dan Layer ditampilkan sebagai struktur utama dalam sidebar kiri.
- Page tetap terlihat ketika Layer dibuka.
- Layer mengikuti halaman aktif.
- Active state halaman dibuat lebih jelas tetapi tetap ringan.
- History dan Page Actions tidak lagi menjadi struktur utama sidebar.

### Panel Layer
- Nama layer menggunakan label yang lebih mudah dipahami.
- Type layer menggunakan icon yang lebih mudah dikenali.
- Selection layer dibuat lebih jelas.
- Kontrol urutan layer tersedia:
  - Paling depan
  - Naik
  - Turun
  - Paling belakang
- Informasi z-index tidak ditampilkan sebagai informasi utama.
- Kontrol urutan dinonaktifkan ketika object sudah berada di batas urutan.

### Sidebar kanan
- Struktur kanan dipusatkan pada KONTEN dan DESAIN.
- Pengaturan layout yang bukan konten object dikeluarkan dari editor Konten yang relevan.
- Pengaturan halaman/canvas berada pada konteks Desain.
- Kondisi tanpa object tetap memiliki konteks desain halaman/canvas.

### Contextual Inspector
- Selection dari canvas dan Layer menggunakan konteks object yang sama.
- Pemilihan object secara default membuka KONTEN.
- Nama dan type object yang dipilih ditampilkan pada inspector.
- Inspector mengikuti type object.
- Group tidak lagi menerima kontrol tipografi yang hanya relevan untuk text.
- Clearing selection mengembalikan konteks halaman/canvas pada Desain.

### Hierarchy dan information density
- Section inspector diubah dari kumpulan card yang padat menjadi struktur yang lebih ringan.
- Nested card dan border yang tidak diperlukan dikurangi.
- Heading section dibuat lebih mudah dipindai.
- Context card yang memiliki fungsi tetap dipertahankan.

### Interaction dan recovery
- Selection canvas dan Layer menggunakan jalur selection yang konsisten.
- Add, duplicate, dan delete page membersihkan selection yang tidak lagi relevan.
- Undo dan Redo membersihkan selection yang tidak lagi valid.
- Layer ordering menggunakan pertukaran urutan agar perpindahan naik/turun dapat dipahami.
- Undo dan Redo dipindahkan ke toolbar EDIT agar lebih mudah ditemukan.
- Control yang sudah berada pada batas urutan dinonaktifkan.

### Scope
- Perubahan UI/UX editor dilakukan langsung pada branch main.
- Tidak dilakukan deployment oleh AI.

## 2. Konten Berdasarkan Layer Terpilih

- Ditambahkan pilihan pada KONTEN untuk:
  - Layer terpilih
  - Semua konten
- Saat Layer terpilih digunakan, editor Konten hanya menampilkan konten yang berkaitan dengan layer tersebut.
- Mode Semua konten tetap tersedia untuk melihat seluruh konten halaman.

## 3. Pagination Langkah Memasak

### Pagination otomatis
- Langkah Memasak dapat dilanjutkan ke halaman A4 berikutnya ketika tidak cukup ruang.
- Pembagian halaman mengikuti tinggi aktual isi, bukan jumlah langkah tetap.
- Judul halaman lanjutan menggunakan penanda “— Lanjutan”.
- Pro Tip ditempatkan pada halaman terakhir dari rangkaian pagination.
- Footer tetap menjadi bagian dari setiap halaman hasil pagination.
- Langkah tetap diperlakukan sebagai satu unit saat pembagian halaman.

### Perbaikan pagination
- Pagination menghitung ulang ketika judul atau deskripsi langkah berubah.
- Data langkah yang berubah tidak dihapus ketika pagination dihitung ulang.
- Rendering pagination diberi perlindungan agar index langkah yang sudah tidak ada tidak dirender.
- Fokus editing langkah dipertahankan ketika perubahan isi menyebabkan langkah berpindah halaman.
- Canvas diarahkan kembali ke langkah yang sedang diedit jika langkah tersebut berpindah dari area yang terlihat.

### Bug halaman kosong
- Diperbaiki bug yang menyebabkan halaman kosong muncul sebelum halaman lanjutan.
- Logika pagination tidak lagi membuat chunk kosong sebelum memindahkan langkah terakhir.
- Penambahan langkah berikutnya tidak lagi bergantung pada halaman kosong tersebut.

### Editor langkah
- Tombol Tambah Langkah berada setelah daftar langkah.
- Tombol Hapus Langkah tersedia pada setiap card langkah.
- Jarak antar-card langkah diperbesar agar setiap langkah lebih mudah dibedakan.
- Tombol Hapus Langkah ditempatkan di sisi kanan heading card.
- Tampilan tombol dan spacing diperbaiki tanpa mengubah fungsi tambah/hapus langkah.

## 4. Status Verifikasi

Yang sudah dapat dinyatakan berdasarkan pekerjaan saat ini:
- Perubahan kode telah dilakukan langsung pada branch main.
- Bug halaman kosong pada pagination telah diuji oleh pengguna dan dinyatakan sudah dapat bekerja.
- Penambahan langkah sudah dilaporkan aman oleh pengguna setelah perbaikan pagination.

Yang belum dinyatakan selesai:
- Verifikasi browser/runtime menyeluruh untuk seluruh pekerjaan UI/UX.
- Verifikasi menyeluruh seluruh kombinasi pagination, export, reload, undo/redo, dan regression.
- Tidak ada klaim bahwa seluruh fitur telah lulus verifikasi hanya berdasarkan perubahan kode.

Dokumen ini sengaja tidak menggunakan checklist centang agar status pekerjaan tidak terlihat lebih terverifikasi daripada kondisi sebenarnya.
