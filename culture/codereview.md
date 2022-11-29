# Code Review through Merge/Pull Request

Code Review berarti mengecek proposal update kode/aplikasi dari Engineer lain. Code Review ini dilakukan melalui Merge Request (MR) di GitLab.

![codereview-screenshot](/images/codereview.png)

## Do(s) and Don't(s)

### Do(s)
1. Relaks, tidak perlu terburu-buru. Review secara hati-hati dan teliti. Memberikan approval dengan sembrono lebih berbahaya dibanding lambat dalam memberikan approval.
2. Jangan berkompromi dengan kualitas. Jangan memberikan approval dengan beberapa catatan konyol seperti, *"MR ini kita merge dulu, kekurangan lainnya bisa lain kali diperbaiki"*. Berikan approval hanya untuk MR yang memberikan kualitas dan value yang bagus.
3. Bagi pembuat MR, patuhi aturan pembuatan MR. Isi checklist MR dengan lengkap dan detail.

### Don't(s)

1. Kode yang diupdate terlalu banyak untuk dimasukkan ke dalam dalam 1 MR. Ingat, Reviewer atau teman sejawat anda juga manusia, dan manusia punya batas ketelitian . Memberikan update yang terlalu banyak dalam 1 MR akan membuat proses review menjadi tidak maksimal.
2. Terlalu bergantung pada Code Review untuk menemukan error. Code Review hanya double check. Pengecekan sesungguhnya mesti dilakukan tiap Engineer di local machine mereka masing-masing. Pastikan dulu kode kita benar, sesuai dengan style guide, testable dan sudah di-test terlebih di local sebelum membuat MR.
3. Memaksa rekan kerja untuk segera melakukan review MR kita. Jangan egois, tiap Engineer mempunyai task yang harus mereka selesaikan. Beri waktu bagi mereka untuk melakukan review.

### MR Template

Tiap kali MR dibuat, pembuat MR harus memastikan item didalam MR Template berikut ini sudah terisi dengan benar dan lengkap. GitLab sendiri mempunyai fitur [MR Template](https://docs.gitlab.com/ee/user/project/description_templates.html) yang dapat kita gunakan.

```markdown
## Make sure MR checklist all checked.
- [ ] Write MR description
- [ ] Unit Testing / Automation Test
- [ ] Code Documentation
- [ ] Rebased with no conflict and no merge history

## What are the problems this MR trying to resolve?
-- Your answer here --

## What are the solutions offered by this MR to solve those problems?
-- Your answer here --

## Type of change
- [ ] Bugs fixes
- [ ] Tweaks
- [ ] New Features
- [ ] Refactor

-- Your answer here. Example: A, B --
## Please attach Youtrack or Redmine issue link
-- Your answer here --

## Does this MR need DevOps Configurations Changes?
If yes, please create new ticket on Redmine and attach the link here

## Have you test this MR on your local? 
-- Your answer here --

## How Has This Been Tested?
Please describe the tests that you ran to verify your changes. Provide instructions so QA can reproduce and review. Please also list any relevant details for your test configuration

## Have you added some documentations regarding these code changes?
-- Your answer here --

**Note:** make sure to execute and the coverage is 100%:
PYTHON_PATH=./src/py poetry run pydocstyle -v --count --max-error-percentage=0 src/py/YOUR_PYTHON_WORKS_FILE_OR_FOLDER`

## Note for Reviewers/Tech Lead
-- Your answer here --
```

### Referensi

Untuk referensi lebih lanjut, lihat video [berikut ini](https://www.youtube.com/watch?v=0t4_MfHgb_A).