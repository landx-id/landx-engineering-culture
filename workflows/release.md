# Release & Deploy

Release dan Deploy adalah bagian penting dari alur kerja Engineer di LandX. Umumnya, tiap Engineer di LandX dalam melakukan release maupun deploy secara mandiri, langsung melalui Discord, dengan menggunakan `landx-bot`. 

## Prerequisites

Sebelum melakukan release maupun deploy, ada beberapa hal yang perlu dipastikan terlebih dahulu oleh Engineer, yaitu:
1. Pastikan *commit* terakhir berhasil di-*build*. Jangan melakukan release jika commit terakhir gagal di-build. Keberhasilan build berarti juga memastikan Docstring dan Coverage Test sudah memenuhi standard, serta Unit Test semua passed.
2. Jalankan End to End Automation Testing. E2E Testing ini harus dijalankan terlebih dahulu untuk memastikan bahwa release terbaru tidak memiliki defect negatif.

## Release

![release-screenshot](/images/release.jpg)

Di LandX, membuat release sama artinya dengan membuat tag. Release artinya menandai sebuah commit dengan label yang human-readable dan mudah diingat. Release dapat dilakukan secara manual di [GitLab](https://gitlab.com/), namun cara ini amat sangat tidak disarankan. Release hendaknya hanya dilakukan melalui `landx-bot`.

### SemVer (Semantic Versioning)

![semver-screenshot](/images/semver.png)

Di LandX, pola penamaan release mengikut format SemVer, yaitu `x.y.z`

`x` artinya versi major. Jika suatu release memiliki penambahan angka pada versi major, itu artinya software tersebut tidak *backward-compatible*. Atau bisa dikatakan terjadi perubahan besar-besaran, atau bisa jadi dilakukan *rewrite* dari *scratch*. 

`y` artinya versi minor. Jika suatu release memiliki penambahan angka pada versi minor, itu artinya pada software tersebut terjadi penambahan fitur, namun masih mempertahankan kompabilitas dengan versi release sebelumnya. 

`z` artinya versi patch. Jika suatu release memiliki penambahan angka pada versi patch, itu artinya pada software tersebut terjadi bug fixing atau tweak kecil.


Referensi: https://semver.org/

### Release with LandX Bot

Dengan menggunakan `landx-bot`, proses release dengan mengikut SemVer ini sangat mudah dilakukan. Engineer tinggal menuliskan perintah berikut pada channel `dev-notif` :

```shell
lx!release <versi: major/minor/patch> <nama aplikasi>
```

Misal, jika ingin merilis suatu versi minor dari aplikasi bernama `landx-web-app`, maka tinggal menuliskan perintah berikut

```shell
lx!release minor landx-web-app
```

Otomatis, `landx-bot` akan memeriksa bagaimana release terakhir kemudian akan membuat tag beserta release di [GitLab](https://gitlab.com/) sesuai dengan format SemVer. Bot akan memberikan notif ketika release sudah dilakukan, lengkap dengan nama versi yang sudah dibuat

![release-1-screenshot](/images/release-1.png)

Sebagai catatan:
1. <nama aplikasi> akan mengikuti format lower-case dengan mengganti spasi menjadi tanda dash (`-`). LandX Web App akan menjadi `landx-web-app`, atau LandX API akan menjadi `landx-api`. 
2. Release secara default akan dilakukan dengan mengambil commit terakhir dari trunk branch (dalam kebanyakan kasus, adalah branch develop).
3. Pada release yang dibuat di GitLab, `Changelog` akan berisi kumpulan commit message yang dibuat dari history commit dari release sebelumnya sampai saat release baru dibuat.

    ![changelog-screenshot](/images/changelog.png)

## Build

Build artinya adalah membuat Docker Image dari aplikasi. Pada umumnya, semua aplikasi (terutama yang berdiri sendiri/Stand Alone), terdapat proses build tiap kali commit ke branch utama (dalam kebanyakan kasus, branch develop). Namun pada kebanyakan kasus, Release akan diikuti oleh Build, yang artinya kita membuat Docker Image spesifik untuk aplikasi dengan versi tertentu.

Untuk melakukan Build aplikasi dengan versi tertentu, pastikan versi tersebut sudah ada, atau dengan kata lain, proses release sudah dilakukan terlebih dahulu sebelum melakukan build. Selanjutnya, tinggal menuliskan perintah berikut ini

```
lx!build <nama aplikasi> <versi>
```

Misalnya, Engineer ingin melakukan Build aplikasi LandX Web App versi `v1.7.3` yang didapat dari proses release sebelumnya, maka Engineer tinggal menulis perintah berikut

```
lx!build landx-web-app v1.7.3
```

![build-screenshot](/images/build.png)

## Deploy

Deploy berarti meng-*install* aplikasi versi tertentu ke Kubernetes. Untuk melakukan Deploy, tentunya harus dipastikan proses Release dan Build sudah dilakukan, karena Deploy memerlukan Docker Image dengan versi tertentu yang sudah berhasil di-*build*. 

Yang harus diperhatikan adalah Deploy tidak bisa dilakukan semata setelah proses Build selesai dilakukan. Engineer harus menunggu hingga proses Build selesai agar Docker Image tersedia dan siap digunakan di proses Deploy.

![deploy-1-screenshot](/images/deploy-1.png)


Untuk melakukan Deploy, Engineer tinggal menulis perintah dengan format berikut di Discord `#dev-notif`

```
lx!deploy <nama aplikasi> <versi> <environment>
```

Environment yang bisa digunakan adalah development, staging, production. Contohnya adalah sebagai berikut

![deploy-screenshot](/images/deploy.png)

Selanjutnya adalah menunggu [ArgoCD](https://argoproj.github.io/cd/) menyelesaikan pekerjaannya untuk men-*deploy* aplikasi hingga muncul notif seperti dibawah ini:


![deploy-2-screenshot](/images/deploy-2.png)


### Deploy with Argo Rollout

Beberapa aplikasi di LandX menggunakan [Canary](/workflows/canary.md) untuk proses deployment. Sehingga proses deploy untuk aplikasi-aplikasi ini memiliki sedikit perbedaan dengan aplikasi lain. Canary Deployment ini di-*handle* oleh [ArgoRollout](https://github.com/argoproj/argo-rollouts/).

Saat men-*deploy* dengan metode Canary, proses deployment tidak langsung selesai begitu Engineer menjalankan perintah `lx!deploy`. Perintah tersebut hanya akan men-*deploy* sebagian kecil Pod (default adalah 25% di Production environment, dan 100% di Staging). Sehingga [ArgoCD](https://argoproj.github.io/cd/) tidak akan memberikan notifikasi bahwa proses deployment selesai dilakukan hingga *rollout* mencapai angka 100%. Untuk itu, Engineer perlu secara bertahap melakukan *rollout* sambil terus memantau error log. 

Untuk melakukan deploy secara bertahap dari 25%, 50%, 75%, hingga 100%, kita dapat menggunakan perintah dibawah ini

```
lx!rollout <nama aplikasi> <environment>
```

Environment yang bisa digunakan adalah development, staging, production. Misalnya

```
lx!rollout landx-web-app production
```

Jika terdapat error pada Pod yang baru dibuat, maka kita dapat melakukan *rollback* atau membatalkan deployment dengan menulis perintah seperti diatas namun dengan tambahan parameter `--rollback`

```
lx!rollout landx-web-app production --rollback
```

Jika kita ingin langsung men-*deploy* aplikasi tanpa melalui tahapan *rollout* kita dapat menggunakan perintah diatas dengan tambahan parameter `--full`

```
lx!rollout landx-web-app production --full
```

#### Undo Rollout

Berbeda dengan rollback yang artinya membatalkan rollout, undo artinya melakukan deploy namun dengan menggunakan versi sebelumnya. Misalkan, pada awalnya kita mempunyai aplikasi LandX Web App v1.7.39 di production dan kita melakukan deploy v1.7.40 hingga tuntas (menggunakan parameter *--full*), kemudian kita ingin kembali menggunakan versi v1.7.39, maka hal ini dapat kita lakukan dengan menggunakan undo.

Untuk melakukan `undo` atau men-deploy aplikasi dengan versi sebelumnya, lakukan perintah berikut ini

```
lx!undo landx-web-app production
```

Perintah diatas akan membuat canary version menjadi v1.7.39 dan stable version di v1.7.40. Selanjutnya, kita dapat melakukan perintah rollout seperti biasa

```
lx!rollout landx-web-app production --full
```

## Monitoring Deployment

Kita dapat memantau proses deploy dengan menggunakan perintah

```
lx!status <nama aplikasi> <environment>
```

![deploy-3-screenshot](/images/deploy-3.png)

Environment yang bisa digunakan adalah development, staging, production. Dari status yang didapat, kita dapat melihat apakah semua Pod berjalan dengan baik atau terdapat error. Jika terdapat error segera lakukan pengecekan.

Untuk mengecek detail deployment pada Canary, gunakan perintah diatas dengan tambahan parameter `--rollout-info`.

![deploy-4-screenshot](/images/deploy-4.png)

## Troubleshooting

Pada proses Release, Build, dan Deploy terkadang terdapat glitch yang membuat proses tersebut gagal. Berikut ini adalah beberapa masalah yang terkadang terjadi dan bagaimana solusinya.

### Error on Release

Meskipun jarang, namun pada beberapa kasus kita menemui kegagalan saat release terutama saat release *patch* version. Kegagalan release ini umumnya disebabkan tag label yang duplikat dikarenakan keterbatasan dari GitLab API yang tidak bisa mengurutkan tag berdasarkan waktu pembuatan (*created_at*). Jika terjadi masalah ini, solusinya ada 2, yaitu
- Menunda release 1 jam kemudian
- Lakukan release minor version