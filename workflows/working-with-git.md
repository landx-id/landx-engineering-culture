# Working with Git

## Git Hooks

### Introduction

There will be pipeline on pre commit and pre push ▶️ **LOCALY**
The code will be be checking **FORMAT**, **LINT**, **DOCUMENTATION** and **UNIT TESTING**
it will give you warning to developer while creating commit and push IF certain condition doesn't meet

### ✅ To apply this SOP you SHOULD:
- Pull latest development code
- execute `make` both inside `./shell` and **outside** shell
- the githooks will trigger every time developer made **commit** or **push**

### ⛔️ NOTE FOR FUTURE SOP
In the future if code already 100% on docs and unit testing, Developer will be **unable** to create any commit or push
if certain condition doesn't meet.

### 📃 PROJECT THAT AFFECTED BY THIS NEW SOP
- landx-web-api
- landx-web-app
- landx-web-dashboard (icx version)

> ▶️ Please apply this sop as soon as possible to avoid more tech-debt and conflict, Thanks 🙇‍♂️

## Commit

Saat bekerja di sebuah ticket, baik di [YouTrack](https://www.jetbrains.com/youtrack/) ataupun [Redmine](https://www.redmine.org/), commit message harus mempunyai referensi ke nomor ticket tersebut, seperti contoh dibawah ini

```
git commit -m "commit message #IssueIDYoutrack"
contoh : git commit -m "update commit #AV3-33"
```

### Convention

Commit convention mengikuti spesifikasi [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/). Untuk memastikan tiap commit memenuhi convention ini, dipasang Githook yang dapat dilihat di [link ini](https://raw.githubusercontent.com/landx-id/Conventional-Commits-Git-Hook/master/commit-msg).
