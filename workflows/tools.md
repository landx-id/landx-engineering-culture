# Developer Tools

## Operating System

Engineer sangat disarankan untuk menggunakan *Nix Based OS seperti Linux atau MacOS. Sangat tidak disarankan menggunakan OS Windows. Semua kode, tools, dan approach di LandX menggunakan sudut pandang penggunaan *Nix-based OS terutama Linux.

Beberapa rekomendasi Linux yang bisa digunakan adalah
1. [Ubuntu](https://ubuntu.com/) 
2. [Linux Mint](https://linuxmint.com/)
3. [Fedora](https://getfedora.org/)
4. [Debian](https://www.debian.org/)

## Git

Git adalah tools yang wajib diinstall oleh tiap Engineer. LandX menggunakan Git sebagai fondasi utama dalam setiap tahapan pengembangan aplikasi. 

Website: https://git-scm.com/

## SSH

SSH diperlukan terutama agar Git yang terinstal di local machine dapat terhubung dengan GitLab.

Referensi: https://ubuntu.com/server/docs/service-openssh

## Docker

Docker adalah bentuk standar dalam distribusi aplikasi. Di LandX, penggunaan Docker adalah wajib. Mulai dari tahap pengembangan aplikasi di [local machine](https://github.com/landx-id/docker-development-environment), proses di [Build Pipeline](/culture/cicd.md), hingga di-*deploy* di environment Staging maupun Production, semuanya menggunakan Docker. 

Website: https://www.docker.com/

## Code Editor

Kita tidak membatasi Code Editor apa yang dipakai. Engineer dapat menggunakan [VSCode](https://code.visualstudio.com/), [Atom Editor](https://atom.io/) atau [Sublime](https://www.sublimetext.com/). Namun dari semua Code Editor yang ada, LandX menyarankan untuk menggunakan Visual Studio Code.

### VS Code

VS Code dapat didownload dan diinstall melalui laman [berikut ini](https://code.visualstudio.com/).

### Plugins

Pemilihan VSCode sebagai default Code Editor di LandX salah satunya adalah keberadaan plugins yang lengkap dan beragam. Plugin ini sangat membantu pekerjaan kita sebagai Engineer di LandX.

Beberapa plugin penting yang perlu diinstall diantaranya adalah:
- [Gitlens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens) - Berguna untuk melihat author dari kode secara realtime
- [GitGraph](https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph) - Visualisasi Git History
- [Flutter](https://marketplace.visualstudio.com/items?itemName=Dart-Code.flutter) - Mendukung pengembangan dan debugging Flutter
- [Robot Framework Intellisense](https://marketplace.visualstudio.com/items?itemName=TomiTurtiainen.rf-intellisense) - Sangat membantu dalam menulis End to End Testing menggunakan [Robot Framework](https://robotframework.org/)
- [Dart](https://marketplace.visualstudio.com/items?itemName=Dart-Code.dart-code) - Syntax highlighting dan Debugging untuk bahasa pemograman Dart
- [Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) - Syntax highlighting dan Debugging untuk bahasa pemograman Python
- [OpenAPI Editor](https://marketplace.visualstudio.com/items?itemName=42Crunch.vscode-openapi) - Mempunyai fitur Swagger Preview yang sangat membantu ketika membuat API Docs menggunakan OpenAPI/Swagger
- [PyLint](https://marketplace.visualstudio.com/items?itemName=ms-python.pylint) - Python Linter and Code Checker