# SILIT — Peraturan Wajib AI Pengerja

## Aturan yang Wajib Dipatuhi

1. Gunakan bahasa sehari-hari.
2. Jangan basa-basi.
3. Gunakan kalimat pendek.
4. Pertahankan angka, requirement, dan constraint penting.
5. Nyatakan apa yang harus dilakukan dan hasilnya.
6. Jangan membuat asumsi.
7. Jangan menebak.
8. Cari weak assumptions dan failure risks.
9. Jangan mengarang weakness.
10. Jelaskan mengapa masalah terjadi dan cara memperbaikinya.
11. Hanya revisi apa yang diminta.
12. Jangan mengubah bagian lain.
13. Jika perubahan lain diperlukan, minta approval.
14. Jangan membuat klaim tanpa verifikasi.
15. Jika informasi tidak cukup, jangan mengarang.
16. Instruksi eksplisit user untuk pekerjaan aktif adalah otoritas utama dalam menentukan kebutuhan dan scope pekerjaan.
17. Jangan meminta approval ulang untuk tindakan yang secara eksplisit sudah diperintahkan user.
18. Jika instruksi eksplisit user bertentangan dengan checklist/dokumentasi lama, sinkronkan dokumentasi yang terdampak sesuai instruksi user, lalu lanjutkan pekerjaan yang diminta.
19. Jangan memakai aturan scope atau checklist untuk menghentikan perintah eksplisit user; gunakan dokumen sebagai panduan kerja dan alat pencatatan status.

## Repository dan Branch

1. `silit` untuk code work.
2. `silitdoc` untuk dokumentasi/checklist.
3. `silit` hanya boleh mempunyai satu branch: `main`.
4. Jangan membuat branch lain.
5. Semua code changes langsung ke `main`.
6. Update `silitdoc` langsung ke `main`.

## Checklist

1. Jangan skipping checklist.
2. Kerjakan checklist sesuai urutan, kecuali instruksi eksplisit user untuk pekerjaan aktif menetapkan kebutuhan yang belum tercakup.
3. Jika ada kebutuhan yang belum tercakup checklist, periksa apakah kebutuhan tersebut sudah diperintahkan secara eksplisit oleh user.
4. Jika sudah diperintahkan secara eksplisit, instruksi tersebut dianggap sebagai approval; sinkronkan checklist/dokumentasi yang terdampak dan lanjutkan tanpa meminta approval ulang.
5. Jika belum diperintahkan secara eksplisit dan benar-benar berada di luar scope, stop dan jelaskan masalah, alasan, serta dampak checklist; minta approval sebelum melanjutkan.
6. Jangan menambah pekerjaan yang tidak diminta user.
7. Hanya update centang checklist untuk pekerjaan yang telah selesai dan diverifikasi.
8. Jangan mengubah wording, urutan, nomor, atau requirement checklist selain bagian yang secara eksplisit perlu disinkronkan dengan instruksi user.

## Riset dan Referensi

1. Research sebelum coding jika pekerjaan membutuhkan reference work.
2. Keputusan design harus mempunyai professional references.
3. Jangan mengarang reference.
4. Jangan mengarang hasil research.
5. Jangan mengarang hasil test.
6. Jangan mengarang hasil pekerjaan.
7. Jangan menyatakan selesai jika belum diverifikasi.

## Perubahan

1. Jangan mengubah bagian yang tidak diminta.
2. Jangan menambah fitur yang tidak diminta.
3. Jangan menghapus fitur yang tidak diminta.
4. Jangan memperluas scope sendiri.
5. Jangan mengganti requirement dengan interpretasi sendiri.
6. Jika perubahan di luar scope diperlukan, stop dan minta approval.

## UI/UX

1. Jika user meminta redesign, jangan hanya melakukan perubahan kecil.
2. Pahami masalah UI/UX sebelum coding jika user meminta audit terlebih dahulu.
3. Jangan coding sebelum audit selesai jika user meminta audit sebelum coding.
4. Keputusan desain harus menggunakan professional references sesuai kebutuhan.
5. Jangan membuat asumsi tentang masalah yang tidak didukung bukti.

## Editor

1. Sidebar kiri adalah `PAGE` dan `LAYER`.
2. Sidebar kanan adalah `KONTEN` dan `DESAIN`.
3. Jangan mengubah struktur tersebut tanpa approval.
4. Jangan mengubah area editor di luar scope tanpa approval.

## Deployment

1. AI tidak boleh melakukan deployment dalam bentuk apa pun.
2. Deployment hanya hak owner.
3. AI tidak boleh melakukan preview deployment.
4. AI tidak boleh melakukan production deployment.
5. AI tidak boleh melakukan staging deployment.
6. AI tidak boleh melakukan redeploy.
7. Jika deployment diperlukan, owner yang melakukan deployment.

## Verifikasi

1. Jangan mengarang result.
2. Jangan mengarang test.
3. Jangan mengklaim sesuatu sudah selesai jika belum diverifikasi.
4. Jika tidak dapat diverifikasi, katakan belum dapat diverifikasi.
5. Jangan mengganti pengujian yang diminta dengan pengujian lain tanpa approval.
6. Jika ada error, gunakan error yang nyata sebagai dasar perbaikan.
