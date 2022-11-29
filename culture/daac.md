# Documentation as a Code

## Intro

DaaC adalah sebuah pendekatan pola pikir yang menegaskan bahwa dokumentasi adalah bagian dari sebuah kode. Terdengar sederhana, namun praktiknya sedikit *tricky*. DaaC akan `"memaksa"` engineer untuk memperlakukan dokumentasi selayaknya mereka memperlakukan source code. Termasuk di dalamnya menggunakan tools yang kerap mereka gunakan ketika bekerja dengan code seperti Versioning Tools, Bug Tracker, Unit Test, dan lain sebagainya.

![daac-screenshot](/images/daac.png)

### Problem

Jika ditanya pertanyaan sederhana seperti *"Apakah Dokumentasi itu penting?"*, rasanya semua orang akan sepakat bahwa jawabannya adalah "Iya, Dokumentasi itu penting". Namun anehnya, meskipun menganggap dokumentasi itu penting, tidak ada engineer yang secara sadar menjadi *obsesif* terhadap dokumentasi. Dengan kata lain, semua engineer sadar jika dokumentasi itu penting, namun malas jika diminta menulis dokumentasi.

Ada beberapa hal yang menyebabkan hal ini terjadi, diantaranya adalah
1. Dokumentasi dianggap sebagai *additional burden* . Pemahaman ini ada karena menganggap bahwa dokumentasi bukanlah code. Jadi, secara natural, engineer akan menganggap bahwa dokumentasi bukan merupakan bagian dari pekerjaan mereka. Menulis dokumentasi artinya mengerjakan hal lain di luar tugas pokok mereka yang mana hal itu tentu saja akan dianggap sebagai beban tambahan dari tugas mereka yang memang sudah berat.
2. Dokumentasi adalah tugas Technical Writer. Anggapan ini tidak sepenuhnya salah, namun juga tidak sepenuhnya benar. Banyak contoh dimana sebuah dokumentasi hanya bisa ditulis oleh engineer seperti misalnya Reference Doc. 

### Solution

DaaC dapat menjadi solusi untuk mengisi kesenjangan antara pentingnya Dokumentasi dan pola pikir engineer. DaaC menganggap bahwa dokumentasi adalah bagian code. Statemen sederhana ini mengubah banyak hal dalam memperlakukan dokumentasi, diantaranya adalah
1. Menulis dokumentasi adalah tugas dari Engineer
2. Dokumentasi harus dimasukkan ke dalam versioning tools
3. Dokumentasi harus dicek serta di-*test* format dan validitasnya. Pengecekan serta test ini dapat dilakukan didalam **Build Pipeline** seperti yang dilakukan terhadap code.
4. Jika dokumentasi tidak sesuai, baik itu format ataupun kontennya, maka hal itu dianggap bug. Bug tersebut harus dicatat di Bug Tracker, di-assign ke Engineer untuk di-solve, dan dicek lagi setelah diperbaiki.

    > The only thing worse than no documentation is bad documentation
    
5. Dokumentasi di-aggregasi kedalam satu *single* portal yang dapat diakses dan direview oleh internal team.


## Technology Stacks

Di LandX, kita menggunakan tools yang sudah kita gunakan untuk source-code, untuk implementasi DaaC.

### GitLab (Code Repository, Code Review, & CI/CD Tools)

Dokumentasi yang menjadi bagian dari sebuah project seperti Readme dan docstring, otomatis akan masuk ke dalam versioning tools. Khusus untuk docstring, kita menggunakan beberapa library untuk melakukan cek dan review. Library yang kita pakai adalah 
- [pydocstyle](https://github.com/landx-id/pydocstyle.git) - Library ini akan memastikan bahwa tiap module dan function memiliki Docstring yang sesuai dengan format. Library ini juga melakukan pengecekan tingkat docstring *coverage* dari sebuah project. Jika *coverage* level berada di bawah batas *treshold* tertentu, aplikasi akan gagal di *build*

    ![daac-2-screenshot](/images/daac-2.png)

- [Sphinx Docs](https://www.sphinx-doc.org/) - Library ini akan meng-generate Docstring menjadi format HTML. File HTML hasil *generate* ini nantinya akan di-*build* menjadi image baru yang akan di-*deploy* ke sebuah subdomain yang bisa diakses oleh internal team.
    ![daac-3-screenshot](/images/daac-3.png)

Untuk aggregasi dokumentasi menjadi sebuah portal, digunakan framework [Docsify](https://docsify.js.org/).

### Redmine

Redmine akan berperan sebagai bug tracker dari dokumentasi yang tidak valid, expired, atau berisi konten yang salah. LandX mempunyai sebuah parent project dan beberapa child project untuk mencatat bug dokumentasi untuk tiap project.

![daac-4-screenshot](/images/daac-4.png)

## Policy

Di LandX Engineering berlaku sebuah aturan tak tertulis terkait DaaC, yaitu 
1. Merge Request tidak akan di-*approve* atau di-*merge* jika Docstring tidak ada
2. Tiap Engineer diharuskan menulis paparan lengkap (terdiri dari ide, konsep, hingga contoh implementasi) saat akan melakukan implementasi dari sebuah fitur. Lihat paparan tentang [VA Payment](/example/va-payment.md) sebagai contohnya.

## Reference

Kita dapat mempelajari lebih dalam tentang konsep di https://cchesser.github.io/docs-as-code/ 

