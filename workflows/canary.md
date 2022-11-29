# Canary Deployment

![canary-screenshot](/images/canary.png)

## Intro

Canary Deployment adalah metode deployment secara staged atau bertahap. Poinnya adalah setiap aplikasi dirilis dengan versi terbaru, kita dapat menentukan seberapa besar porsi User yang menerima update dari rilis tersebut. Hal ini akan sangat berguna, karena kita dapat memonitor bagaimana rilis terbaru ini bekerja.

Jika terdapat error, hanya sebagian kecil dari user yang mendapat error tersebut dan kita dapat dengan mudah melakukan rollback atau membatalkan rilis tersebut. 

## Implementation

LandX mengimplementasikan Canary Deployment melalui [Argo Rollout](https://github.com/argoproj/argo-rollouts).

Code Snippet berikut memperlihatkan bagaimana implement Canary Deployment menggunakan Argo Rollout pada aplikasi LandX Web App

```yaml
---
apiVersion: argoproj.io/v1alpha1
kind: Rollout
metadata:
  name: landx-web-app
spec:
  replicas: 3
  strategy:
    canary:
      steps:
        - setWeight: 25
        - pause: {}
        - setWeight: 50
        - pause: {}
        - setWeight: 75
        - pause: {}
  selector:
    matchLabels:
      app: landx-web-app
  template:
    spec:
      containers:
        - name: landx-web-app
          image: asia.gcr.io/landx/landx-web-app:v0.2.4
          imagePullPolicy: Always
```

Terlihat pada potongan konfigurasi diatas, secara default, saat aplikasi dirilis, sistem akan mengatur agar 25% dari seluruh request yang masuk akan diarahkan ke versi terbaru. Sisanya, sebesar 75% akan masuk ke versi lama. Secara bertahap dengan melalui command [Discord Bot](/workflows/discord-bot.md), Engineer dapat melakukan rollout secara bertahap dari *25%*, *50%*, *75%*, sampai pada akhirnya **100%** yang artinya semua request akan masuk ke versi terbaru, dan aplikasi versi lama akan dimatikan.

## Canary Deployment on Mobile App

Untuk aplikasi Android dan iOS, LandX menggunakan metode Canary Deployment bawaan dari Google Play dan AppStore. Pada Google Play, misalnya, kita dapat mengatur persentase rollout yang akan membatasi jumlah User yang dapat melakukan update.

Lebih jelasnya tentang Staged Rollout di PlayStore dapat dilihat pada tautan [berikut ini](https://support.google.com/googleplay/android-developer/answer/6346149?hl=en).