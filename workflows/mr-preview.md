# MR Preview

![mr-preview-screenshot](/images/mr-preview.jpeg)

## Background

QA/Tech Lead, pernah ga ngerasa ribet sewaktu ngecek/nge-review Pull Request? Ribet karena harus buka halaman Pull Request terlebih dahulu, pull ke local, run di local, baru kemudian di-cek apakah sudah sesuai atau belum.

Bagi sebagian besar Lead, dalam sehari mereka bisa mengecek lebih dari 5 Pull Request dan langkah-langkah diatas harus dilakukan secara repetitif.

Untuk solve problem diatas, kami menggunakan metode Pull Request Preview. Kami menggunakan Nginx Proxy yang memudahkan saya untuk membuat dynamic URL yang unik untuk tiap Pull Request.

Konsepnya dapat dilihat digambar diatas. Cukup sederhana, ketika ada Engineer yang membuat Pull Request, secara otomatis akan mengirim sebuah Web Hook yang akan men-trigger Build System untuk nge-build image untuk Pull Request tersebut. Selesai build, notifikasi akan dikirim ke Preview Server yang akan langsung mendownload dan menjalankan docker image, serta mengekspose URL unik yang dapat diakses oleh TL/QA untuk melakukan review Pull Request.

## Implementation

Untuk menggunakan MR Preview, terdapat 2 cara. Cara pertama adalah menambahkan label `preview` saat membuat Merge Request.

![mr-preview-1-screenshot](/images/mr-preview-1.png)

Cara lain adalah dengan melalui *landx-bot*

```
lx!preview <nama aplikasi> <ID MR>
```

![mr-preview-2-screenshot](/images/mr-preview-2.png)

![mr-preview-3-screenshot](/images/mr-preview-3.png)

## Reference
1. Library Nginx Proxy: https://github.com/nginx-proxy/nginx-proxy