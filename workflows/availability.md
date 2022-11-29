# Availability

## Implementation

Availability tim Engineering bisa diatur melalui [landx-bot](/workflows/discord-bot.md) dengan mengirim pesan private ke bot atau via channel ***#dev-notif*** dengan format:

Ketika ingin off atau unavailable

```bash
lx!me off --message=<message>
```

Ketika ingin on atau available kembali

```bash
lx!me on
```

Misalnya, ketika seorang Engineer cuti dua hari, maka ia bisa set availability dengan perintah berikut ini

```bash
lx!me off --message="Cuti 2 hari, tanggal 20-22 Agustus 2022"
```

Atau ketika ingin off selama 3 jam di hari tersebut

```bash
lx!me off --message="Off jam 1-3, pergi ke pasar"
```

Ketika sudah available kembali, bisa menjalankan perintah

```bash
lx!me on
```

Saat availability di set off, maka ketika engineer tersebut di-*mention* di semua channel, landx-bot secara otomatis akan membalas pesan tersebut seperti dibawah ini:

```
@glend is unavailable: Off jam 1-3, pergi ke pasar
```
