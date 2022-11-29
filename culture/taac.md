# Test as a Code

![automation-testing-screenshot](/images/automation-testing.png)

Di LandX, ada dua jenis test yang dilakukan. Pertama adalah Manual Testing. Manual Testing adalah test yang dilakukan secara manual oleh QA maupun Engineer. Engineer harus melakukan manual testing terlebih dahulu di local machine masing-masing sebelum melakukan push code ke repository. Selanjutnya, QA akan melakukan manual testing, baik di environment Staging maupun Production. QA akan melakukan serangkaian manual testing per fitur hingga UAT yang akan memastikan apakah sebuah fitur dapat di-deploy di Production. Selain itu, QA melakukan manual testing secara berkala di Production, terutama di bagian-bagian kritikal dari aplikasi.

Jenis Testing kedua adalah Automation Testing. Automation Testing ini dibagi menjadi 3: Unit Testing, End2End Testing, dan Load Testing.

## Unit Testing

Scope dari Unit Testing adalah function. Engineer akan menguji tiap function yang mereka tulis. Build Pipeline akan menjalankan Unit Testing ini di tiap commit di *develop* branch dan Merge Requests. Code Coverage untuk Unit Testing harus mencapai treshold tertentu (umumnya berada pada kisaran 70%-80%) agar Build Pipeline dapat selesai dengan sukses. Berikut ini adalah potongan gambar dari rangkaian Build Pipeline yang mensyaratkan Unit Testing agar proses build dapat selesai dengan sukses.

![taac-screenshot](/images/taac.png)

## E2E Testing

E2E Testing sebagian besar ditulis QA untuk menggantikan proses manual dari skenario testing yang dimiliki oleh QA. E2E Testing akan berjalan di environment Staging. Untuk menjalankannya, dapat melalui `landx-bot` :

![taac-1-screenshot](/images/taac-1.png)

Hasil testing akan diupload secara otomatis di sebuah storage, dan landx-bot akan kembali mengirim notifikasi pada Discord.

## Load Testing

Load Testing digunakan untuk menguji ketahanan sebuah sistem. Saat melakukan Load Testing, sangat disarankan untuk mengisolasi environment testing agar tidak mengganggu eksisting sistem. Di LandX, kami mempunyai isolated environment dimana kami dapat melakukan Load Testing sewaktu-waktu. Sama seperti E2E Testing, Load Testing dapat dilakukan dengan bantuan *landx-bot* seperti pada gambar dibawah ini.

![taac-2-screenshot](/images/taac-2.png)

## Technology Stacks

1. Unit Testing: [PyTest](https://docs.pytest.org/)
2. End-2-End Testing: [Robot Framework](https://robotframework.org/) dengan [Selenium](https://github.com/robotframework/SeleniumLibrary/)
3. Load Testing: [Locust](https://locust.io/)