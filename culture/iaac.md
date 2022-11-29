# Infrastucture as a Code

![iaac-screenshot](/images/iaac.png)

## Intro

IaaC adalah sebuah pendekatan dalam membangun infrastruktur melalui code. Sebelum ada pendekatan ini, cara untuk membangun sebuah infrastuktur adalah melalui setting manual. Cara yang lebih canggih adalah dengan membuat script yang berisi perintah untuk men-setup infrastruktur. IaaC membawa cara ini ke level yang berbeda. Alih-alih membuat script atau men-setup infrastuktur secara manual, IaaC memungkinkan kita untuk mendefinisikan infrastuktur yang kita inginkan dalam bentuk kode.

Kubernetes misalnya, menggunakan konfigurasi dalam bentuk yaml untuk mendefinisikan cluster beserta isinya, lengkap dengan segala konfigurasi yang kita inginkan.

## Goals

IaaC mempunyai banyak kelebihan dibandingkan cara lama dalam membuat infrastruktur, yaitu diantaranya:

1. Reproduce Infrastuktur menjadi jauh lebih mudah dan cepat. Katakanlah, kita ingin menghapus infrastruktur yang kita punya saat ini dan membuatnya kembali dari awal. IaaC memungkinkan kita membuat kembali infrastruktur yang persis sama dengan mudah dan cepat. Hal ini dimungkinkan karena melalui IaaC, infrastuktur didefinisikan dalam bentuk kode.
2. Auditable. Infrastruktur yang dibuat dengan pendekatan IaaC dapat di-audit dengan mudah. Sekali lagi, karena infrastruktur didefinisikan dalam bentuk kode, kita dapat melihat semua pemakaian resource di kode tersebut.

## Technology Stacks

Dalam implementasi IaaC ini, LandX menggunakan beberapa teknologi dibawah ini

1. [Docker](https://www.docker.com/)
2. [Kubernetes](https://kubernetes.io/)