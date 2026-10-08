# SILIT — Peraturan Wajib AI Pengerja

## Status Dokumen

- Dokumen ini berisi peraturan wajib yang harus dipatuhi AI saat mengerjakan project SILIT.
- Peraturan ini bersifat wajib.
- AI tidak boleh mengabaikan peraturan ini karena alasan teknis, kenyamanan, kecepatan, atau asumsi sendiri.
- Jika ada konflik atau kebutuhan baru yang berada di luar aturan ini, AI harus berhenti dan meminta persetujuan.
- Dokumen ini tidak boleh diubah setelah dibuat.
- Hanya checklist pengerjaan yang boleh diperbarui jika dokumen ini memiliki checklist pekerjaan.
- Tidak boleh menambah, menghapus, atau menulis ulang peraturan secara sepihak.

---

# 1. Prinsip Kerja Dasar

1. Jangan membuat asumsi.
2. Jangan menebak.
3. Jangan mengarang hasil, data, referensi, pengujian, atau kondisi sistem.
4. Jika informasi tidak cukup, katakan bahwa informasinya belum cukup.
5. Jika sesuatu belum diverifikasi, jangan menyatakan bahwa sesuatu tersebut sudah selesai, benar, aman, atau berhasil.
6. Setiap klaim tentang hasil pekerjaan harus berdasarkan verifikasi nyata.
7. Jika menemukan kelemahan atau risiko, jelaskan berdasarkan bukti yang tersedia.
8. Jangan mengarang kelemahan hanya untuk terlihat melakukan audit.
9. Jelaskan alasan masalah dan cara memperbaikinya.
10. Utamakan ketepatan dibanding kecepatan.
11. Patuhi instruksi user secara langsung.
12. Jangan malas dengan mengganti pekerjaan yang diminta menjadi jawaban umum atau rencana yang tidak diminta.

---

# 2. Aturan Perubahan Kode

1. Hanya ubah bagian yang diminta.
2. Jangan mengubah bagian lain yang tidak termasuk scope.
3. Jangan melakukan refactor yang tidak diminta.
4. Jangan menambah fitur di luar scope.
5. Jangan menghapus fitur yang tidak diminta.
6. Jangan mengubah angka, requirement, constraint, atau perilaku yang sudah ditentukan tanpa persetujuan.
7. Jika perubahan yang diperlukan ternyata menyentuh area di luar scope, berhenti dan minta persetujuan terlebih dahulu.
8. Jangan menggunakan perubahan kosmetik untuk menyatakan bahwa sebuah redesign sudah selesai.
9. Jika user meminta redesign, pahami perubahan struktur, hierarchy, information architecture, dan interaction model yang diperlukan; jangan hanya mengganti warna, spacing, border, atau sedikit CSS.
10. Perubahan UI/UX harus mempunyai alasan desain yang jelas.
11. Untuk keputusan desain yang membutuhkan referensi profesional, lakukan riset referensi profesional sebelum coding.
12. Jangan mengklaim sebuah desain mengikuti Figma, Nielsen, Don Norman, Alan Cooper, Aza Raskin, atau referensi lain jika dasar klaim tersebut tidak benar-benar tersedia.
13. Jangan membuat teori atau prinsip yang tidak didukung sumber ketika mengatasnamakan ahli.
14. Jika sumber tidak cukup, nyatakan keterbatasannya.

---

# 3. Aturan Repository SILIT

1. Repository kode utama adalah `silit`.
2. GitHub repository: `omegasands87/silit`.
3. Semua pekerjaan kode dilakukan di repository `silit`.
4. Branch repository `silit` hanya boleh satu: `main`.
5. Jangan membuat branch lain.
6. Semua perubahan kode langsung ke `main`.
7. Jangan menggunakan branch sementara.
8. Jangan membuat workflow yang membutuhkan branch tambahan.
9. Jangan melakukan deployment dalam bentuk apa pun.
10. AI dilarang melakukan deploy.
11. AI dilarang melakukan preview deployment.
12. AI dilarang melakukan production deployment.
13. AI dilarang melakukan staging deployment.
14. AI dilarang melakukan redeploy.
15. AI dilarang memicu deployment Vercel secara langsung maupun tidak langsung.
16. Deployment adalah hak owner.
17. Walaupun deployment diperlukan untuk memeriksa hasil, AI tetap tidak boleh melakukan deployment.
18. Jika perlu deployment untuk verifikasi, jelaskan bahwa owner yang harus melakukan deployment.

---

# 4. Aturan Vercel

1. Vercel hanya boleh digunakan untuk pemeriksaan yang tidak melakukan deployment jika tool yang tersedia memungkinkan.
2. Jangan membuat deployment.
3. Jangan promote deployment.
4. Jangan redeploy.
5. Jangan trigger build/deployment melalui API atau action yang menghasilkan deployment.
6. Jangan menganggap URL production berubah hanya karena kode sudah diubah di GitHub.
7. Jangan menyatakan hasil production sudah menggunakan kode terbaru jika belum diverifikasi.
8. Jika user memberikan hasil build/deployment dari Vercel, gunakan hasil tersebut sebagai bukti sesuai konteksnya.
9. Jika build gagal, jangan menyatakan pekerjaan berhasil.
10. Perbaiki error berdasarkan error nyata yang tersedia, bukan tebakan.

---

# 5. Aturan Dokumentasi SILITDOC

1. Repository dokumentasi adalah `silitdoc`.
2. GitHub repository: `omegasands87/silitdoc`.
3. `silitdoc` digunakan untuk dokumentasi dan checklist.
4. Pekerjaan kode tidak dilakukan di `silitdoc`.
5. Semua update dokumentasi dilakukan langsung ke branch `main`.
6. Jangan membuat branch lain di `silitdoc`.
7. Dokumentasi yang dinyatakan sebagai dokumen tetap tidak boleh ditulis ulang.
8. Jika user menetapkan dokumen sebagai dokumen yang tidak boleh diubah, aturan tersebut mutlak.
9. Untuk dokumen yang dikunci, hanya checkbox checklist pengerjaan yang boleh diperbarui jika memang diizinkan oleh user.
10. Jangan mengubah wording checklist.
11. Jangan mengubah urutan checklist.
12. Jangan mengubah nomor checklist.
13. Jangan mengubah requirement checklist.
14. Jangan menambah item checklist ke dokumen yang sudah dikunci.
15. Jangan menghapus item checklist dari dokumen yang sudah dikunci.
16. Jangan memindahkan item checklist.
17. Jangan mengganti isi dokumentasi dengan versi baru.
18. Checkbox hanya boleh dicentang setelah pekerjaan benar-benar selesai dan diverifikasi.
19. Jangan mencentang berdasarkan asumsi.
20. Jangan mencentang berdasarkan niat.
21. Jangan mencentang hanya karena kode sudah ditulis.
22. Jangan mencentang hanya karena perubahan terlihat masuk akal.
23. Jangan mencentang jika pengujian yang diwajibkan belum dilakukan.
24. Checklist lama tidak boleh diubah kecuali update centang pekerjaan yang benar-benar telah selesai dan diverifikasi.
25. Jangan mengubah isi checklist lama untuk menyesuaikan hasil pekerjaan.

---

# 6. Aturan Urutan Checklist

1. Checklist harus dikerjakan sesuai urutan yang sudah ditentukan.
2. Jangan melewati checklist.
3. Jangan mengerjakan item berikutnya lalu menganggap item sebelumnya otomatis selesai.
4. Jika item sebelumnya belum selesai atau belum diverifikasi, jangan menyatakan tahap berikutnya selesai.
5. Jika muncul pekerjaan baru yang tidak ada dalam checklist, hentikan proses.
6. Jelaskan masalah baru tersebut.
7. Jelaskan alasannya.
8. Jelaskan checklist yang terdampak.
9. Ajukan perubahan yang diperlukan.
10. Tunggu persetujuan user sebelum mengubah scope.
11. Jangan memasukkan fitur baru ke checklist tanpa persetujuan.

---

# 7. Aturan Verifikasi

1. Verifikasi harus dilakukan dengan alat atau bukti yang benar-benar tersedia.
2. Jangan mengklaim browser test jika tidak melakukan browser test.
3. Jangan mengklaim build pass jika build belum dijalankan atau belum ada bukti build pass.
4. Jangan mengklaim runtime tidak error jika runtime belum diperiksa.
5. Jangan mengklaim visual match tanpa visual yang benar-benar diperiksa.
6. Jangan mengklaim export benar tanpa file export yang benar-benar diperiksa jika pemeriksaan file merupakan requirement.
7. Jangan mengklaim regression test selesai jika semua langkah yang diwajibkan belum diverifikasi.
8. Bedakan dengan jelas antara:
   - sudah diubah
   - sudah diverifikasi
   - belum diuji
   - gagal
   - tidak dapat diuji dengan tool yang tersedia
9. Jika tool tidak tersedia untuk sebuah pengujian, katakan bahwa pengujian tersebut belum dapat diverifikasi.
10. Jangan mengganti pengujian yang diminta dengan pengujian lain lalu menyatakan hasilnya setara.

---

# 8. Aturan Audit UI/UX

1. Audit harus membedakan masalah visual, information architecture, hierarchy, interaction, dan usability.
2. Jangan menyebut masalah hanya berdasarkan selera pribadi.
3. Untuk keputusan desain yang membutuhkan dasar profesional, gunakan referensi profesional.
4. Jangan mengubah UI sebelum audit atau dasar perubahan dijelaskan jika user meminta audit terlebih dahulu.
5. Jika user meminta audit sebelum coding, audit harus selesai dan dijelaskan sebelum kode diubah.
6. Jika user meminta dokumentasi audit, dokumentasikan masalah yang benar-benar ditemukan.
7. Jangan membuat audit palsu untuk membenarkan perubahan yang sudah dibuat.
8. Jika desain sebelumnya ternyata salah, akui kesalahan tersebut dan jelaskan masalahnya.
9. Jangan menganggap perubahan kecil sebagai redesign penuh.
10. Redesign harus mempertimbangkan:
    - information architecture
    - hierarchy
    - mental model
    - context
    - recognition vs recall
    - visibility of system status
    - user control
    - consistency
    - error prevention
    - flexibility
    - minimalist presentation
11. Jangan menggunakan nama ahli sebagai hiasan. Setiap atribusi harus mempunyai dasar sumber.
12. Jangan mengarang prinsip Aza Raskin atau ahli lain jika sumber tidak mendukungnya.

---

# 9. Aturan Scope Editor

1. Sidebar kiri adalah area PAGE dan LAYER sesuai keputusan desain yang telah ditetapkan.
2. Sidebar kanan adalah area KONTEN dan DESAIN sesuai keputusan desain yang telah ditetapkan.
3. Layer tidak boleh dipindahkan kembali menjadi tab utama sidebar kanan tanpa persetujuan.
4. Perbaikan audit harus menyelesaikan masalah struktur, bukan sekadar kosmetik.
5. PAGE → LAYER → SELECTED OBJECT → DESIGN PROPERTIES harus menjadi mental model yang jelas.
6. Saat tidak ada selection, panel desain harus tetap mempunyai konteks yang berguna.
7. Saat ada selection, inspector harus mengikuti object yang dipilih.
8. Page/canvas properties tidak boleh salah diklasifikasikan sebagai object content.
9. Layer harus diperlakukan sebagai struktur visual, bukan daftar detail implementasi.
10. Informasi teknis seperti z-index tidak boleh menjadi informasi utama jika tidak dibutuhkan pengguna.
11. Selection dari canvas dan Layer harus memiliki hubungan yang jelas dengan inspector.
12. Perubahan sidebar tidak boleh merusak fitur editor yang berada di luar scope.

---

# 10. Aturan Referensi Profesional

1. Jika user meminta desain berdasarkan referensi profesional, lakukan riset sebelum coding.
2. Referensi harus relevan dengan keputusan yang akan dibuat.
3. Jangan menggunakan referensi hanya sebagai formalitas.
4. Jangan mengklaim bahwa sebuah UI sama dengan produk profesional tanpa verifikasi.
5. Jika menggunakan Figma sebagai referensi, hanya klaim bagian yang benar-benar didukung sumber Figma.
6. Jika menggunakan Nielsen/NN-g sebagai referensi, hanya klaim heuristik yang benar-benar didukung sumber NN-g.
7. Jika menggunakan Alan Cooper, jangan mengarang prinsip yang tidak didukung sumber.
8. Jika sumber tidak cukup kuat, nyatakan bahwa dasar tersebut tidak cukup.

---

# 11. Aturan Perubahan Terhadap Bagian Lain

1. Jangan menyentuh toolbar jika user tidak meminta toolbar.
2. Jangan menyentuh canvas jika user tidak meminta canvas.
3. Jangan menyentuh export jika user tidak meminta export.
4. Jangan menyentuh fitur image editing jika user tidak meminta image editing.
5. Jangan menyentuh history jika user tidak meminta history.
6. Jangan menyentuh page system jika perubahan tersebut tidak diperlukan oleh scope yang sedang dikerjakan.
7. Jika sebuah perubahan UI membutuhkan perubahan area lain, berhenti dan minta persetujuan.
8. Jangan memperluas scope hanya karena menemukan sesuatu yang menurut AI lebih bagus.

---

# 12. Aturan Komunikasi Hasil

1. Jawaban harus langsung ke inti.
2. Gunakan bahasa sehari-hari.
3. Gunakan kalimat pendek.
4. Jangan basa-basi.
5. Pertahankan angka, requirement, dan constraint penting.
6. Sebutkan apa yang harus dilakukan.
7. Sebutkan hasil yang benar-benar sudah dicapai.
8. Pisahkan hasil yang sudah diverifikasi dari yang belum.
9. Jangan menutupi kegagalan.
10. Jika terjadi error, jelaskan error tersebut secara langsung.
11. Jika belum bisa diverifikasi, katakan belum bisa diverifikasi.
12. Jangan menggunakan kata "selesai" jika pekerjaan belum benar-benar selesai.

---

# 13. Aturan Untuk Perubahan yang Memerlukan Persetujuan

Persetujuan user wajib diminta jika:

1. scope harus diperluas;
2. checklist harus diubah;
3. requirement harus diubah;
4. struktur repository harus diubah;
5. branch baru diperlukan;
6. area editor di luar scope harus diubah;
7. fitur baru perlu ditambahkan;
8. fitur lama perlu dihapus;
9. dokumentasi yang dikunci perlu diubah;
10. perubahan teknis memiliki dampak yang tidak dapat dihindari ke area lain.

Tanpa persetujuan, AI harus berhenti pada titik tersebut.

---

# 14. Aturan Khusus Saat Ada Error Build

1. Gunakan error yang benar-benar diberikan sebagai dasar.
2. Lokasi file dan nomor baris harus diperiksa.
3. Struktur kode terkait harus diperiksa sebelum memperbaiki.
4. Jangan membuat perbaikan berdasarkan tebakan.
5. Setelah perbaikan, verifikasi ulang dengan metode yang tersedia.
6. Jangan menyatakan build berhasil sebelum ada bukti.
7. Jangan melakukan deployment untuk membuktikan build.

---

# 15. Aturan Khusus Untuk Checklist Pekerjaan

1. Checklist adalah alat status pekerjaan, bukan tempat menulis ulang requirement.
2. Centang hanya pekerjaan yang benar-benar selesai.
3. Setiap centang harus mempunyai bukti.
4. Jangan mencentang beberapa item sekaligus hanya karena dianggap saling berkaitan.
5. Jangan menganggap satu test membuktikan semua item.
6. Jika hanya sebagian item terverifikasi, hanya bagian yang benar-benar terverifikasi yang boleh dicentang.
7. Jangan menghapus centang tanpa alasan dan persetujuan jika status tersebut sudah ditetapkan.
8. Jangan mengubah wording checklist untuk membuat pekerjaan terlihat selesai.

---

# 16. Aturan Mutlak Deployment

1. AI tidak boleh melakukan deployment dalam kondisi apa pun.
2. Tidak boleh deploy production.
3. Tidak boleh deploy preview.
4. Tidak boleh deploy staging.
5. Tidak boleh redeploy.
6. Tidak boleh promote deployment.
7. Tidak boleh trigger deployment melalui API.
8. Tidak boleh menggunakan tool Vercel untuk menghasilkan deployment.
9. Tidak boleh melakukan deployment secara tidak langsung melalui automation.
10. Owner adalah satu-satunya pihak yang melakukan deployment.
11. Jika user meminta AI melakukan deployment, AI harus menolak bagian deployment tersebut dan tetap menjaga perubahan kode sesuai scope.

---

# 17. Aturan Mutlak Dokumentasi Terkunci

1. Dokumen yang sudah dinyatakan user sebagai tidak boleh diubah adalah immutable.
2. AI tidak boleh mengedit isinya.
3. AI tidak boleh memperbaiki wording sendiri.
4. AI tidak boleh menambahkan klarifikasi sendiri.
5. AI tidak boleh menghapus bagian yang dianggap redundant.
6. AI tidak boleh mengubah urutan.
7. AI tidak boleh mengganti checklist.
8. Jika dokumentasi perlu perubahan, minta persetujuan user terlebih dahulu.
9. Jika user mengizinkan perubahan, ikuti persis perubahan yang diminta dan jangan mengubah bagian lain.

---

# 18. Prinsip Akhir

AI wajib bekerja berdasarkan:

**Bukti → Scope → Referensi → Implementasi → Verifikasi → Checklist**

Bukan:

**Asumsi → Coding → Klaim selesai**

Jika bukti tidak cukup, jangan mengarang.

Jika scope tidak jelas, jangan memperluas.

Jika perubahan membutuhkan persetujuan, berhenti dan minta persetujuan.

Jika pekerjaan belum diverifikasi, jangan mencentang.

Jika user menetapkan dokumen sebagai immutable, jangan mengubahnya.

Jika deployment diperlukan, owner yang melakukan deployment.

