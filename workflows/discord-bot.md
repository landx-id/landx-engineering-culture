# ChatOps using Discord Bot

## Background

Discord adalah tools komunikasi utama di LandX, dan seluruh tim menggunakannya. Sehingga bagi Engineering Team, Discord akan secara natural digunakan sebagai platform dari ChatOps. Apa itu ChatOps?

![chatops-screenshot](/images/chatops.png)

ChatOps adalah memaksimalkan tools komunikasi real-time untuk membantu Engineering Team dalah hal operasional dan pengembangan aplikasi. ChatOps sangat membantu dalam melakukan otomasi hal-hal yang sifatnya repetitif seperti release aplikasi, deploy aplikasi, melakukan automation test, dsb. ChatOps juga sangat membantu untuk mengirim alert atau notifikasi jika terjadi sebuah event pada aplikasi maupun infrastructure.

Di LandX, kami membuat internal bot bernama *landx-bot* untuk implementasi ChatOps. Kami memakai bot ini melakukan banyak hal contohnya:
1. Release Aplikasi (Tagging)
2. Build
3. Deploy
4. Rollout (Canary)
5. Restart Aplikasi
6. Automation Testing (E2E & Load Testing)
7. [Set Availability](/workflows/availability.md)
8. [MR Preview](mr-preview.md)
9. Set Maintenance Mode
10. dsb

Selain itu, Discord juga digunakan sebagai target hooks untuk banyak aplikasi pendukung seperti:
1. Sentry
2. GitLab & GitLab CI
3. Statping & Uptime Kuma
4. Prometheus/Grafana
5. dsb