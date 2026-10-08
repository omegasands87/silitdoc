# SILIT — Referensi Pengerjaan UI/UX

## Tujuan

Dokumen ini menjadi referensi untuk pekerjaan UI/UX SILIT.

Isi diambil dari sumber yang relevan untuk tokoh yang sebelumnya diberikan:

- Don Norman
- Jakob Nielsen
- Alan Cooper
- Aza Raskin

Dokumen ini tidak dimaksudkan untuk mengarang prinsip baru atas nama tokoh-tokoh tersebut.

---

# 1. Don Norman

## Inti Referensi

### 1.1 Signifier harus membantu pengguna mengetahui apa yang bisa dilakukan

Don Norman menjelaskan bahwa pada interface digital, yang penting bagi pengguna adalah tanda atau petunjuk yang dapat dipersepsikan untuk memahami tindakan yang tersedia.

Implikasi untuk UI:

- Control harus terlihat sebagai control.
- Pengguna harus dapat mengetahui tindakan yang tersedia.
- Tampilan harus memberikan petunjuk yang cukup.
- Jangan membuat pengguna menebak fungsi suatu elemen.

Sumber: Don Norman, "Signifiers, not affordances".  
urlSumber Don Norman — Signifiers, not affordanceshttps://jnd.org/signifiers-not-affordances/

### 1.2 Gunakan conceptual model yang koheren

Norman menekankan pentingnya conceptual model yang jelas dan konsisten.

Interface yang berbeda bagian tetapi menggunakan logika yang berbeda akan membuat pengguna sulit membangun mental model.

Implikasi untuk UI:

- Struktur harus mempunyai logika yang jelas.
- Bagian interface yang memiliki fungsi serupa harus mengikuti pola yang konsisten.
- Perubahan context harus dapat dipahami.
- Struktur informasi harus membantu pengguna membangun mental model.

Sumber: Don Norman, "Design as Communication".  
urlSumber Don Norman — Design as Communicationhttps://jnd.org/design-as-communication/

### 1.3 Gunakan convention dengan hati-hati

Norman menjelaskan bahwa convention yang sudah dikenal pengguna menjadi constraint yang membantu pengguna memahami interface.

Implikasi untuk UI:

- Jangan mengubah pola yang sudah umum tanpa alasan kuat.
- Jika menggunakan pola baru, pengguna tetap membutuhkan petunjuk yang jelas.
- Konsistensi membantu pengguna memahami tindakan.

Sumber: Don Norman, "Affordance, Conventions and Design".  
urlSumber Don Norman — Affordance, Conventions and Designhttps://jnd.org/affordance-conventions-and-design-part-2/

### Inti yang dipakai untuk SILIT

**UI harus memberi petunjuk yang terlihat, memiliki conceptual model yang koheren, dan menggunakan convention secara konsisten.**

---

# 2. Jakob Nielsen

## Inti Referensi

Nielsen memiliki 10 usability heuristics. Untuk pengerjaan UI/UX SILIT, seluruh 10 heuristics menjadi dasar evaluasi.

### 2.1 Visibility of System Status

Pengguna harus mengetahui apa yang sedang terjadi melalui feedback yang sesuai.

Untuk SILIT:

- page aktif harus jelas;
- object terpilih harus jelas;
- tab aktif harus jelas;
- perubahan state harus terlihat.

### 2.2 Match Between System and the Real World

Interface harus menggunakan bahasa dan konsep yang mudah dipahami pengguna, bukan jargon internal.

Untuk SILIT:

- hindari istilah teknis sebagai informasi utama jika ada istilah pengguna yang lebih jelas;
- gunakan label yang menggambarkan fungsi sebenarnya.

### 2.3 User Control and Freedom

Pengguna membutuhkan kontrol dan jalan keluar dari tindakan yang tidak diinginkan.

Untuk SILIT:

- perpindahan context harus mudah;
- action penting harus mudah dikendalikan;
- pengguna tidak boleh terjebak pada state tertentu.

### 2.4 Consistency and Standards

Hal yang sama harus terlihat dan bekerja dengan cara yang konsisten.

Untuk SILIT:

- selection state konsisten;
- active state konsisten;
- istilah konsisten;
- struktur panel konsisten.

### 2.5 Error Prevention

Lebih baik mencegah error daripada hanya menampilkan error setelah terjadi.

Untuk SILIT:

- control yang tidak relevan jangan menjadi fokus utama;
- context editing harus jelas;
- struktur UI harus mengurangi kemungkinan salah edit.

### 2.6 Recognition Rather Than Recall

Pengguna sebaiknya mengenali pilihan dan informasi daripada harus mengingatnya.

Untuk SILIT:

- status penting harus terlihat;
- context object yang dipilih harus terlihat;
- fungsi panel harus mudah dikenali;
- jangan memaksa pengguna mengingat state sebelumnya.

### 2.7 Flexibility and Efficiency of Use

Interface harus dapat digunakan secara efisien oleh pengguna dengan tingkat pengalaman berbeda.

Untuk SILIT:

- action utama harus mudah ditemukan;
- selection dari canvas atau layer harus membawa context yang benar;
- pengguna tidak perlu melakukan navigasi berulang yang tidak perlu.

### 2.8 Aesthetic and Minimalist Design

Interface tidak seharusnya berisi informasi yang tidak relevan karena setiap informasi tambahan bersaing dengan informasi yang relevan.

Untuk SILIT:

- kurangi informasi teknis yang tidak diperlukan;
- kurangi nested card yang tidak memiliki fungsi;
- kurangi visual noise;
- prioritaskan property dan action yang relevan.

### 2.9 Recognize, Diagnose, and Recover from Errors

Pesan error harus mudah dipahami dan membantu pengguna mengetahui masalah serta solusi.

Untuk SILIT:

- error harus menggunakan bahasa yang jelas;
- masalah harus dapat dikenali;
- recovery harus jelas jika memang diperlukan.

### 2.10 Help and Documentation

Interface sebaiknya dapat digunakan tanpa dokumentasi tambahan, tetapi dokumentasi tetap diperlukan ketika memang dibutuhkan.

Untuk SILIT:

- fungsi utama harus dapat dipahami dari UI;
- dokumentasi digunakan sebagai bantuan, bukan pengganti desain yang jelas.

Sumber utama: Nielsen Norman Group, "10 Usability Heuristics for User Interface Design".  
urlSumber Jakob Nielsen — 10 Usability Heuristicshttps://www.nngroup.com/articles/ten-usability-heuristics/

Ringkasan resmi heuristics:  
urlNielsen Norman Group — Heuristic Summaryhttps://media.nngroup.com/media/articles/attachments/NNg_Jakob%27s_Usability_Heuristic_Summary.pdf

---

# 3. Alan Cooper

## Inti Referensi

### 3.1 Design harus berorientasi pada goals pengguna

Alan Cooper menggunakan pendekatan Goal-Directed Design.

Fokusnya bukan hanya siapa pengguna atau task apa yang dilakukan, tetapi tujuan yang ingin dicapai pengguna.

Untuk SILIT:

- pahami tujuan pengguna ketika menggunakan editor;
- desain interaction berdasarkan tujuan tersebut;
- jangan membuat interface hanya berdasarkan struktur internal aplikasi.

### 3.2 Persona bukan pengguna rata-rata

Dalam pendekatan Cooper, persona adalah archetype yang memiliki karakteristik, goals, behavior, dan context yang spesifik.

Persona bukan sekadar label seperti "user" atau "admin".

### 3.3 Persona harus berdasarkan research, bukan asumsi

Sumber yang menjelaskan pendekatan Cooper menekankan bahwa persona yang baik dibangun dari data dan research pengguna.

Untuk SILIT:

- jangan membuat kebutuhan pengguna berdasarkan tebakan;
- jangan menganggap semua pengguna mempunyai tujuan yang sama;
- jika persona digunakan, dasar persona harus jelas.

### 3.4 Context dan behavior penting

Goal-Directed Design memperhatikan:

- goals;
- behavior;
- context;
- workflow;
- attitudes;
- hubungan pengguna dengan produk.

Untuk SILIT:

- evaluasi panel berdasarkan pekerjaan yang benar-benar ingin dilakukan pengguna;
- jangan hanya menilai panel dari tampilan visualnya.

Sumber: Interaction Design Foundation, "Personas — The Encyclopedia of Human-Computer Interaction".  
urlSumber Alan Cooper — Goal-Directed Personashttps://ixdf.org/literature/book/the-encyclopedia-of-human-computer-interaction-2nd-ed/personas

Sumber tambahan: Center Centre, wawancara tentang Goal-Directed Design.  
urlCenter Centre — Goal-Directed Designhttps://articles.centercentre.com/goal_directed_design/

### Inti yang dipakai untuk SILIT

**Desain harus berangkat dari tujuan, behavior, dan context pengguna; bukan dari asumsi tentang pengguna.**

---

# 4. Aza Raskin

## Batasan Sumber

Untuk Aza Raskin, sumber yang kuat dan relevan dengan materi yang sebelumnya diberikan terutama berkaitan dengan **Infinite Scroll**.

Tidak cukup dasar untuk mengatribusikan teori UI/UX lain kepadanya hanya berdasarkan gambar atau reputasi.

Karena itu dokumen ini tidak akan mengarang prinsip lain atas nama Aza Raskin.

## 4.1 Infinite Scroll menghilangkan stopping cue

Infinite scroll membuat konten terus berlanjut tanpa titik akhir yang jelas.

Salah satu dampaknya adalah pengguna kehilangan natural stopping point yang sebelumnya diberikan oleh pagination.

## 4.2 Mengurangi friction tidak selalu berarti UX lebih baik

Infinite scroll awalnya mengurangi friction seperti klik "next page".

Namun pola yang sama dapat menghasilkan konsekuensi berbeda ketika digunakan untuk sistem yang bertujuan mempertahankan perhatian pengguna.

Untuk SILIT:

- jangan menganggap setiap pengurangan langkah otomatis lebih baik;
- evaluasi apakah friction yang dihilangkan memang mengganggu tujuan pengguna;
- perhatikan apakah suatu pola menghilangkan kontrol atau stopping point yang berguna.

Sumber yang membahas Aza Raskin dan konsekuensi Infinite Scroll:  
urlRaskin Center — Aza Raskin, Infinite Scroll, and a Family Argument About Attentionhttps://raskincenter.org/ideas/aza-raskin-infinite-scroll/

## Batas penggunaan referensi Aza Raskin

Untuk pekerjaan SILIT, jangan menyatakan bahwa Aza Raskin mengajarkan prinsip tertentu selain yang benar-benar didukung sumber.

Jika tidak ada sumber yang cukup, jangan membuat atribusi.

---

# 5. Sintesis Untuk Pengerjaan UI/UX SILIT

Bagian ini adalah **sintesis dari sumber di atas**, bukan kutipan atau teori baru yang diatribusikan kepada satu tokoh.

## 5.1 Understandability

Interface harus dapat dipahami dari tanda, label, struktur, dan feedback yang tersedia.

Dasar:
- Don Norman
- Jakob Nielsen

## 5.2 Consistent Mental Model

Struktur interface harus memiliki logika yang konsisten sehingga pengguna dapat membangun mental model yang stabil.

Dasar:
- Don Norman
- Jakob Nielsen

## 5.3 User Goal

UI harus membantu pengguna mencapai tujuan mereka, bukan memaksa pengguna mengikuti struktur internal aplikasi.

Dasar:
- Alan Cooper
- Don Norman

## 5.4 Recognition

Informasi penting harus terlihat sehingga pengguna tidak perlu mengingat context sebelumnya.

Dasar:
- Jakob Nielsen

## 5.5 Visible Actions

Tindakan yang tersedia harus mempunyai petunjuk yang dapat dikenali.

Dasar:
- Don Norman
- Jakob Nielsen

## 5.6 Minimal Information

Informasi yang tidak relevan tidak boleh mengambil perhatian dari informasi yang relevan.

Dasar:
- Jakob Nielsen

## 5.7 User Control

Efisiensi tidak boleh dicapai dengan menghilangkan kontrol yang penting bagi pengguna.

Dasar:
- Jakob Nielsen
- pembelajaran dari pembahasan Aza Raskin tentang Infinite Scroll

## 5.8 Research Before Assumption

Keputusan tentang pengguna tidak boleh dibuat hanya berdasarkan asumsi.

Dasar:
- Alan Cooper
- Don Norman

---

# 6. Aturan Penggunaan Referensi Ini

1. Referensi ini digunakan sebagai dasar evaluasi dan keputusan UI/UX.
2. Jangan mengatribusikan sintesis pada tokoh tertentu.
3. Jika sebuah keputusan tidak didukung oleh sumber di dokumen ini, jangan mengklaim bahwa keputusan tersebut berasal dari tokoh tersebut.
4. Jika sumber tidak cukup untuk suatu kesimpulan, nyatakan bahwa sumber tidak cukup.
5. Jangan mengembangkan teori baru lalu memasukkannya sebagai teori tokoh.
6. Referensi tidak menggantikan verifikasi terhadap UI SILIT yang sebenarnya.
7. Keputusan akhir harus tetap berdasarkan scope pekerjaan dan bukti dari editor SILIT.

---

# 7. Daftar Sumber

### Don Norman

- urlJND.org — Signifiers, not affordanceshttps://jnd.org/signifiers-not-affordances/
- urlJND.org — Affordances and Designhttps://jnd.org/affordances-and-design/
- urlJND.org — Design as Communicationhttps://jnd.org/design-as-communication/
- urlJND.org — Affordance, Conventions and Designhttps://jnd.org/affordance-conventions-and-design-part-2/

### Jakob Nielsen

- urlNielsen Norman Group — 10 Usability Heuristics for User Interface Designhttps://www.nngroup.com/articles/ten-usability-heuristics/
- urlNielsen Norman Group — Heuristic Summaryhttps://media.nngroup.com/media/articles/attachments/NNg_Jakob%27s_Usability_Heuristic_Summary.pdf

### Alan Cooper

- urlInteraction Design Foundation — Personashttps://ixdf.org/literature/book/the-encyclopedia-of-human-computer-interaction-2nd-ed/personas
- urlCenter Centre — Goal-Directed Designhttps://articles.centercentre.com/goal_directed_design/

### Aza Raskin

- urlRaskin Center — Aza Raskin, Infinite Scroll, and a Family Argument About Attentionhttps://raskincenter.org/ideas/aza-raskin-infinite-scroll/
