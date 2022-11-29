# Developer KPI

![kpi-screenshot](/images/kpi.png)

## Use Case

KPI diperlukan untuk mengukur tingkat produktivitas dari tiap Engineer, secara perorangan. LandX memang sudah mempunyai OKR sebagai salah satu alat ukur pencapaian, namun OKR saja dirasa tidak cukup karena OKR tidak dapat digunakan untuk mengukur produktivitas seorang Engineer secara akurat.

KPI ini dibuat agar dapat menjadi patokan dalam pengambilan keputusan terkait perpanjangan kontrak, promosi, demosi, ataupun pemutusan kerja.

## Component

Komponen yang digunakan untuk mengukur KPI adalah sebagai berikut:
1. `Coding Activities` - Sebagai seorang developer, aktivitas utama harian adalah coding. Maka aktivitas coding sudah tentu akan menjadi salah satu penilaian utama dari seorang Developer. Hal yang dilihat disini misalnya adalah commit, kualitas kode yang diberikan, dan aktivitas di sebuah Merge Request (diskusi, code review, dsb).
2. `Accomplishment` - Item ini mengukur pencapaian seorang developer pada suatu project. Penyelesaian project secara berkualitas, ketepatan waktu delivery, dan effort yang diberikan dalam project tersebut adalah hal-hal yang dinilai dari komponen ini.
3. `Attitude` - Attitude adalah sikap dari seorang developer dalam kesehariannya, termasuk di dalamnya seperti level ownership terhadap product, availability dalam meeting atau diskusi terkait product, dan komunikasi sehari-hari.

## Implementasi

Sumber penilaian yang kuantitatif seperti commit dan keaktifan di MR akan diekstrak dari GitLab, YouTrack, dan Redmine. Sedangkan penilaian yang bersifat kualitatif seperti Attitude akan bersifat subyektif, baik dari sisi Tech Leads ataupun developer itu sendiri, dengan perhitungan bobot sebagai berikut:
1. **Kuantitatif**: 45%
2. **Subyektif Tech Leads/Head of Engineering**: 49%
3. **Subyektif Developer**: 6%

Tiap bulan, akan di-*compile* data dari sumber penilaian kuantitatif untuk dilihat apakah ada developer dengan skor KPI yang rendah. Hasil penilaian kuantitatif ini akan digabungkan dengan judgement secara subyektif dari Tech Leads dan konfirmasi dari Developer terkait dan rekan setimnya, untuk kemudian dapat diambil keputusan terkait rendahnya skor Developer tersebut.