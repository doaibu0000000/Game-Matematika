# Kali 1–10 — Game Perkalian (PWA)

Game matematika perkalian 1–10 untuk anak-anak. Bisa **di-install di Android** seperti aplikasi biasa dan tetap **berjalan tanpa internet** (offline). Siap di-deploy ke **GitHub Pages**.

## Fitur

- Pilih tabel perkalian 1–10, atau campur semua
- 2 mode: **Latihan** (10 soal, tanpa waktu) dan **Tantangan** (60 detik)
- Skor + bonus streak 🔥, rekor tersimpan di perangkat (localStorage)
- Efek suara (Web Audio, tanpa file) dan getar (vibrasi HP)
- PWA lengkap: manifest + service worker → bisa di-install & offline
- Murni HTML + CSS + JavaScript, **tanpa framework dan tanpa build step**

## Struktur file

```
.
├── index.html                  # aplikasi (HTML + CSS + JS dalam satu file)
├── manifest.json               # metadata PWA
├── sw.js                       # service worker (cache offline)
├── icons/                      # ikon aplikasi (PNG)
│   ├── icon-192.png
│   ├── icon-512.png
│   ├── icon-maskable-192.png
│   ├── icon-maskable-512.png
│   └── apple-touch-icon.png
├── .nojekyll                   # matikan pemrosesan Jekyll di GitHub Pages
└── README.md
```

Semua path memakai `./` (relatif), jadi aman untuk URL subfolder GitHub Pages seperti `https://username.github.io/nama-repo/`.

## Deploy ke GitHub Pages

1. Buat repository baru di GitHub, misalnya `game-perkalian`.
2. Upload/push semua file ini ke branch `main` — pastikan `index.html` berada di **root** repository, bukan di dalam subfolder.
3. Buka **Settings → Pages** di repository.
4. Pada bagian **Build and deployment → Source**, pilih **Deploy from a branch**.
5. Pilih branch `main` dan folder `/ (root)`, lalu klik **Save**.
6. Tunggu 1–2 menit, situs akan aktif di:
   `https://USERNAME.github.io/game-perkalian/`

Cara push dari komputer (jika belum):

```bash
git init
git add .
git commit -m "Game perkalian 1-10 (PWA)"
git branch -M main
git remote add origin https://github.com/USERNAME/game-perkalian.git
git push -u origin main
```

## Install di Android

1. Buka alamat situsnya di **Chrome** di HP Android.
2. Ketuk tombol **⬇️ Install Aplikasi** yang muncul di halaman utama
   (atau menu ⋮ Chrome → *Tambahkan ke layar utama*).
3. Selesai — ikon aplikasi muncul di layar utama, jalan layar penuh, dan bisa dibuka tanpa internet.

> Catatan: tombol install hanya muncul setelah situs dibuka lewat **https** (GitHub Pages sudah otomatis https) dan setelah service worker terdaftar (buka halaman sekali, tunggu beberapa detik).

**iPhone/iPad:** buka di Safari → tombol *Bagikan* → *Tambahkan ke Layar Utama*.

## Update aplikasi

Jika mengubah `index.html`, ikon, atau file lain, **naikkan versi cache** di `sw.js` agar semua pengguna mendapat versi baru:

```js
const CACHE_NAME = 'kali10-v1';   // ubah menjadi 'kali10-v2', dst.
```

## Testing lokal (opsional)

Service worker hanya aktif lewat `http://localhost` atau `https`, bukan lewat `file://`:

```bash
python -m http.server 8080
# lalu buka http://localhost:8080
```
