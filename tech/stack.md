# Stack

LandX Engineering menggunakan beberapa Technology Stack dalam pengembangan aplikasi. Walaupun begitu, kita berusaha untuk selalu meminimalisir ragam teknologi yang kita gunakan. Tujuan akhirnya adalah simplicity, maintanability, serta memudahkan setiap engineer untuk bisa berkontribusi di semua project yang ada di LandX.

## Programming Language

### Python

Python adalah bahasa pemograman utama di LandX Engineering. Kita menggunakannya di beberapa aplikasi utama termasuk aplikasi monolithic utama kita yaitu LandX Web App. Python adalah bahasa pemograman yang sangat mudah untuk dipelajari dan mempunyai ketersediaan library/package yang sangat beragam untuk memenuhi hampir semua kebutuhan dalam membangun aplikasi.

Versi Python yang kita gunakan adalah versi **Python 3.9.9**

Ref: [https://www.python.org/](https://www.python.org/)

#### Flask

Flask adalah framework Python yang kita gunakan untuk mengembangkan aplikasi Web dan Backend. Bersama [Jinja](https://jinja.palletsprojects.com/) kita menggunakannya sebagai FullStack Framework untuk mengembangkan aplikasi berbasis web.

Ref: [https://flask.palletsprojects.com/](https://flask.palletsprojects.com/)

### JavaScript/TypeScript

Dalam mengembangkan aplikasi, terutama aplikasi web, JavaScript adalah bahasa pemograman yang tidak bisa kita abaikan. Kita menggunakannya terutama untuk mengembangkan Frontend Web.

Ref: 
- JavaScript: [https://developer.mozilla.org/en-US/docs/Web/JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
- TypeScript: [https://www.typescriptlang.org/](https://www.typescriptlang.org/)

#### ReactJS

ReactJS adalah salah satu JS Framework utama yang kita gunakan. Kita menggunakannya sebagai Frontend Framework di aplikasi utama kita yaitu LandX Web App. Meskipun begitu, kita tidak menggunakan ReactJS sebagai suatu framework utuh di Frontend, namun kita menggabungkannya dengan Jinja (Flask) sebagai bagian dari sistem untuk me-render tampilan web.

Ref: [https://reactjs.org/](https://reactjs.org/)

#### Svelte

Selain ReactJS, kami juga menggunakan Svelte sebagai alternatif JS Framework untuk Frontend. Svelte termasuk framework yang relatif baru di ekosistem JavaScript, sehingga secara internal, penggunaan Svelte bisa juga dikatakan sebagai suatu eksprimen yang patut untuk dicoba. Jika hasilnya bagus, maka kita akan menggunakannya di proyek-proyek di masa depan.

Ref: [https://svelte.dev/](https://svelte.dev/)

### Erlang

Erlang digunakan sebagai bahasa pemograman untuk membangun core system di LandX, yaitu **hanya** di bagian transaksi jual-beli lot (Exchange System).

Ref: [https://www.erlang.org/](https://www.erlang.org/)

## Styling

### Tailwind

Untuk CSS, LandX menggunakan Tailwind sebagai CSS Framework utama. Tailwind digunakan di eksisting aplikasi yang sudah ada dan juga akan digunakan di aplikasi-aplikasi yang akan dibuat dimasa depan

Ref: https://tailwindcss.com/

## Database

LandX menggunakan beberapa database sesuai dengan kebutuhan. Database yang digunakan ada yang bertipe relasional (RDBMS) ataupun NoSQL. 

### PostgreSQL

PostgreSQL digunakan sebagai database yang utama di LandX. Semua aplikasi standalone dan vital akan menggunakan PostgsqSQL sebagai penyimpanan data. LandX menggunakan Managed PostgreSQL yang di-host di [CloudSQL](/cloud/gcp/intro.md). PostgreSQL yang digunakan adalah PostgreSQL v11.

Ref: https://www.postgresql.org/

### MongoDB

MongoDB digunakan untuk menyimpan data non-core atau data pendamping yang tidak terlalu vital semisal data catatan aktivitas user. MongoDB diinstall didalam cluster Kubernetes pada namespace `mongodb`. MongoDB yang digunakan adalah versi 4.
Ref: https://www.mongodb.com/

## Cache

Cache digunakan di banyak tempat. Hampir semua aplikasi standalone menggunakan cache, baik itu native cache dari Python ataupun memanfaatkan software khusus seperti penggunaan Redis.

### Redis

Redis digunakan sebagai cache dan juga in-memory database semisal untuk menyimpan session. Redis diinstall di dalam cluster Kubernetes. Namun, tidak seperti MongoDB, dimana terdapat namespace khusus untuk instalasinya, Redis diinstal di tiap namespace yang membutuhkannya.

Ref: https://redis.io/

## Deployment

LandX mengikuti standard industri terkini untuk deployment, seperti penggunaan Docker dan Kubernetes.

### Docker

Di LandX, Docker adalah standard format distribusi dari sebuah aplikasi. Artinya, aplikasi harus di-*dockerize* terlebih dahulu untuk bisa di-*deploy*. 

Ref: https://www.docker.com/

### Kubernetes

Kubernetes adalah Container Orchestrator yang digunakan di LandX, bisa dikatakan sebagai sistem operasi cloud dari hampir semua aplikasi yang dikembangkan di LandX. Kubernetes memberikan tim Engineering fleksibilitas dalam hal development, deployment, scaling, hingan maintainance aplikasi.

Ref: https://kubernetes.io/

## Project Management

### YouTrack

Ref: https://www.jetbrains.com/youtrack/

### Redmine

Ref: https://www.redmine.org/

## Error Tracking, Alert, & APM

### Sentry
Ref: https://sentry.io/