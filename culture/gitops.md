# GitOps

![gitops-screenshot](/images/gitops.png)

## Intro

GitOps adalah implementasi lanjutan dari IaaC. Dalam [IaaC](/culture/iaac.md), kita dapat mendefinisikan infrastuktur dalam bentuk kode, namun ada beberapa lubang disini. Bagaimana misalnya:

1. Jika kode konfigurasi harus di-share ke orang lain?
2. Jika kode konfigurasi dimiliki oleh beberapa orang, dan salah satu dari pemilik kode tersebut mengubah sekaligus mengeksekusi perubahan tersebut, namun tidak memberikan update tersebut ke pemilik lain?

Disini, GitOps menutup lubang tersebut dengan memberikan beberapa persyaratan terkait kode konfigurasi, diantaranya:

1. Semua kode konfigurasi harus disatukan dalam satu tempat
2. Kode konfigurasi yang sudah disatukan dalam satu tempat tersebut harus di-track perubahannya ke dalam Git
3. Tidak diperbolehkan untuk merubah dan langsung melakukan eksekusi terhadap suatu konfigurasi, melainkan semua perubahan tersebut harus di-commit dan di push ke git repository.

Sebagai lanjutan terhadap poin 3 diatas, nantinya akan ada sebuah *tool* yang secara kontinu melakukan scanning terhadap Git repository dari kode konfigurasi yang kita miliki. Jika terdapat perubahan pada Git repository, *tool* inilah yang mengeksekusi perubahan konfigurasi tersebut.

## Goals

Goals dari GitOps adalah memastikan bahwa infrastruktur eksisting yang kita miliki saat ini sama persis dengan apa yang didefinisikan di git repository dari kode konfigurasi untuk membangun infrastruktur tersebut. GitOps menghilangkan perbedaan versi antara kode konfigurasi dengan infrastruktur yang berjalan sekarang. Dapat dikatakan bahwa dengan GitOps, kita menggunakan git repository sebagai *single of truth*, dari infrastruktur yang berjalan saat ini.

Selain itu, dengan GitOps, kita dapat mengetahui riwayat dari perubahan infrastruktur beserta siapa yang melakukan perubahan tersebut.

## Technology Stacks

Untuk GitOps, LandX menggunakan [ArgoCD](https://argoproj.github.io/cd/). 

## Implementations

Terdapat sebuah repo untuk menampung semua konfigurasi yang berada di repository bernama `infra-codes`. Untuk melakukan perubahan, update konfigurasi, commit, dan push ke `infra-codes` repository. ArgoCD akan menjalankan tugasnya untuk mengupdate infrastruktur sesuai dengan perubahan yang telah dibuat.