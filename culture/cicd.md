# CI/CD - Continuous Integration & Continuous Delivery

![cicd-screenshot](/images/cicd.png)

## Intro

CI/CD adalah sebuah metode untuk men-*deliver* aplikasi secara berkelanjutan ke User, dengan menggunakan banyak otomasi di tiap tahap pengembangan aplikasi. LandX menggunakan metode ini dalam pengembangan aplikasi. Implementasi tidak hanya dilakukan melalui tools atau software, namun juga terwujud dalam kultur sehari-hari.

## Goals

Dari sudut pandang Engineering Team, goal utama dari CI/CD adalah memastikan aplikasi selalu dalam *state* **RELEASABLE**. Artinya, aplikasi dapat di-*deploy* kapan pun. LandX mengimplementasikan banyak hal untuk mendukung tujuan ini. Mulai dari pemakaian versioning tools, membuat Build Pipeline, mewajibkan Engineer untuk menulis Automation Test (End to End maupun Unit Test), dan membuat [Bot Discord](/workflows/discord-bot.md) yang memungkinkan Engineer untuk dapat men-*deploy* aplikasi secara mudah dan mandiri.

## Implementations

### Versioning Control System

LandX menggunakan self-hosted [GitLab](https://gitlab.com/) sebagai VCS tools. GitLab memiliki fitur yang lengkap dan sejauh ini cukup mengakomodasi kebutuhan internal team terkait dengan VCS.

### Trunk-Based Development

![tbd-screenshot](/images/trunk-based-development.png)

Trunk-Based Development adalah praktik penggunaan Git yang hanya memakai satu branch utama yang disebut Trunk (di LandX, kita memakai branch *develop*). Semua Merge Request hanya mengarah ke branch utama tersebut. Tidak ada branch lain yang digunakan sebagai target Merge Request yang mengakibatkan adanya lebih dari satu branch yang terus terupdate secara paralel. Sehingga semua release/tag creation sumbernya hanya satu, yaitu branch utama.

Penggunaan Trunk-Based Development ini secara langsung meng-*enforce* Engineer untuk memastika kode yang di-*push* adalah kode yang berkualitas dan tidak membawa dampak negatif ke kode eksisting.

#### Case Study : LandX Web App v3

Pada LandX Web App v3, terjadi perubahan yang cukup signifikan terutama dari sisi tampilan, meskipun ada juga perubahan dari sisi flow. Bagaimana implementasi trunk-based development untuk kasus ini?

***Pertama***, kita tidak menggunakan branch lain untuk pengembangan v3. Branch utama yang digunakan tetap `develop`, jadi semua MR harus mengarah ke branch *develop*.

***Kedua***, buat versioning untuk routing. Hal ini mudah dilakukan, cukup dengan membuat blueprint yang baru untuk v3 seperti terlihat pada snippet dibawah ini

```python
LOGIN_BLUEPRINT_V3 = Blueprint("login", __name__, url_prefix="/v3/login")
LOGIN_BLUEPRINT_V3.add_url_rule("/", "index", index.login, methods=["GET", "POST"])
LOGIN_BLUEPRINT_V3.add_url_rule("/logout", "logout", logout, methods=["GET"])

```

***Ketiga***, usahakan semaksimal mungkin untuk *reuse* eksisting *function* atau *class*. Jika terdapat perbedaan logic atau kode di flow yang baru, buat function lagi dengan suffix `_v3`

```python
def _login_user_v3(user_obj):
    # do something
```

Setelah itu, tandai *function* lama dengan *decorator* `deprecated`. Kita bisa menggunakan library seperti [Flask-Deprecated](https://pypi.org/project/flask-deprecate/) atau membuat decorator sendiri secara manual.


```python
@deprecate_route("This will removed once v3 is launched")
def _login_user(user_obj):
    # do something
```

***Keempat***, untuk view atau HTML template atau JS script, buat file baru dengan suffix `_v3`. 

***Kelima***, ketika v3 sudah dirilis, hapus semua function dengan decorator `deprecated`, file view yang mempunyai 'kembaran' dengan suffix `_v3`, dan juga file blueprint.

***Keenam***, gunakan [Feature Toggle](/workflows/feature-toggle.md) untuk menyembunyikan routing agar tidak dapat diakse selama masa development

```python
if is_flag_enable('v3_enabled'):
    LOGIN_BLUEPRINT_V3.add_url_rule("/", "index", index.login, methods=["GET", "POST"])
```


### Build Pipeline

LandX menggunakan [GitLab CI](https://docs.gitlab.com/ee/ci/) sebagai build tools. Tiap commit ataupun release pada aplikasi akan melewati sejumlah tahapan sampai pada akhirnya aplikasi dapat di-*build* secara sempurna. Secara umum, tahapan dalam Build Pipeline di LandX adalah
1. **Test** - Di tahap ini, akan dijalankan beberapa Automation Test dan Automation Check. Contoh Automation Test yang akan dijalankan adalah Unit Test. Sedangkan contoh Automation Check adalah pengecekan Docstring, Secret Detection (mencegah variable sensitif ter-*commit*), dsb. Intinya, proses ini akan memastikan bahwa kode yang di-*commit* sudah well-tested dan sesuai dengan Style/Coding Guide yang telah disepakati. Jika tahapan ini gagal, maka proses Build akan berhenti disini.
2. **Build** - Tahapan ini adalah yang utama dalam proses di Pipeline, karena di tahapan inilah aplikasi akan di-*build* ke dalam bentuk Docker Image. Pasca Image berhasil di-*build*, Image tersebut kemudian akan di-*push* ke [Container Registry](https://docs.gitlab.com/ee/user/packages/container_registry/).
3. **Verify** - Di tahap ini dilakukan beberapa verifikasi, seperti misalnya Container Scanning (Image yang sudah berhasil di-*build* akan dicek apakah memiliki vulnerability issue) dan Code Scanning menggunakan [SonarQube](https://www.sonarqube.org/) untuk memerika apakah kode di aplikasi memiliki kemungkinan bug dan vulnerability issue.

Build Pipeline akan berjalan secara otomatis dengan **2 trigger utama**: commit ke develop branch dan tag creation/application release.

### Automation Test

LandX mewajibkan tiap Engineer untuk menulis test, yang meliputi Unit Test dan End to End Testing. Tiap hari, Engineer menambahkan kode ke dalam repository dalam bentuk pembuatan fitur, memperbaiki bugs, atau bahkan melakukan *refactor*. Automation Test akan memastikan bahwa tiap penambahan kode tidak akan mempunyai implikasi negatif ke kode eksisting. Hal ini akan menambah rasa percaya diri dalam internal team dan membuat tim lebih *agile* dalam bekerja.

### Deployment

LandX memiliki Deployment System yang serba otomatis. Dengan memanfaatkan integrasi yang maksimal antara [GitLab](https://gitlab.com/) - [GitOps](/culture/gitops.md) menggunakan [ArgoCD](https://argoproj.github.io/cd/) - [Discord Bot](/workflows/discord-bot.md), kita memiliki alur deployment yang smooth dan mudah digunakan oleh semua Engineer. Engineer dapat melakukan release dan deploy secara mandiri langsung dari Discord.

### Canary Deployment

Lebih jelas tentang Canary Deployment dapat dilihat [disini](/workflows/canary.md).