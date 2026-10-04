# Kali Master — Game Perkalian 1–25 (PWA)

Game matematika perkalian bergaya **petualangan 3.500 level (35.000 soal)** dengan **sistem pangkat naik seperti catur** sampai **Grand Master**. Bisa **di-install di Android** seperti aplikasi biasa dan tetap **berjalan tanpa internet** (offline). Siap di-deploy ke **GitHub Pages**.

## Fitur

- **🗺️ Mode Petualangan — 3.500 level / 35.000 soal** dalam 5 tingkat: Mudah 🟢 → Normal 🔵 → Sulit 🟠 → Ekstrim 🟣 → Tingkat Terakhir 🔴
- **Setiap tingkat berisi 7.000 soal** (700 level × 10 soal), peta level berhalaman seperti game puzzle
- **Level terbuka berurutan**: lulus level (≥7 benar dari 10 soal) untuk membuka level berikutnya; tingkat baru terbuka setelah 7.000 soal tingkat sebelumnya tuntas
- **Bintang ⭐⭐⭐** per level: ★★★ = 9–10 benar, ★★ = 8 benar, ★ = 7 benar
- **🎓 Latihan Bebas**: pilih sendiri jangkauan (1–10 / 1–20), tabel, dan mode (Latihan / Tantangan 60 detik)
- **10 tingkatan pangkat** seperti catur — naik dengan mengumpulkan XP
- Skor + bonus streak 🔥, rekor tersimpan di perangkat
- Efek suara (Web Audio, tanpa file) dan getar (vibrasi HP)
- PWA lengkap: manifest + service worker → bisa di-install & offline
- Murni HTML + CSS + JavaScript, **tanpa framework dan tanpa build step**

## Petualangan: isi tiap tingkat (700 level = 7.000 soal per tingkat)

| Tingkat | Isi soal | Poin per jawaban benar |
|---|---|---|
| 🟢 Mudah | mulai 1–2 × 1–6, naik bertahap sampai 1–5 × 1–10 | 10 |
| 🔵 Normal | mulai 2–6 × 2–6, naik sampai 2–10 × 2–10 | 15 |
| 🟠 Sulit | mulai 3–9 × 3–9, naik sampai 3–12 × 3–15 | 20 |
| 🟣 Ekstrim | mulai 8–12 × 8–12, naik sampai 8–20 × 8–20 | 25 |
| 🔴 Tingkat Terakhir | mulai 12–16 × 12–16, naik sampai 12–25 × 12–25 | 30 |

Tiap level = 10 soal pilihan ganda. Level `n` dalam satu tingkat memakai rentang angka yang sedikit lebih luas dari level `n−1`, jadi kesulitan naik perlahan sepanjang 700 level. Peta level dibagi per halaman (50 level per halaman) dengan navigasi |◀ ◀ ▶ ▶| seperti game puzzle.

## Tingkatan pangkat

XP = akumulasi skor dari semua permainan (petualangan maupun latihan bebas). Total XP seluruh petualangan ± 800.000.

| Pangkat | Ikon | XP dibutuhkan |
|---|---|---|
| Pemula | 🐣 | 0 |
| Pion | ♟️ | 500 |
| Kuda | 🐴 | 2.500 |
| Benteng | 🏰 | 7.500 |
| Gajah | 🐘 | 20.000 |
| Menteri | 👸 | 45.000 |
| Calon Master | 🎖️ | 90.000 |
| Master | 🥈 | 180.000 |
| Master Besar | 🥇 | 350.000 |
| **Grand Master** | 👑 | **600.000** |

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

1. Buat repository baru di GitHub, misalnya `kali-master`.
2. Upload/push semua file ini ke branch `main` — pastikan `index.html` berada di **root** repository, bukan di dalam subfolder.
3. Buka **Settings → Pages** di repository.
4. Pada bagian **Build and deployment → Source**, pilih **Deploy from a branch**.
5. Pilih branch `main` dan folder `/ (root)`, lalu klik **Save**.
6. Tunggu 1–2 menit, situs akan aktif di:
   `https://USERNAME.github.io/kali-master/`

Cara push dari komputer (jika belum):

```bash
git init
git add .
git commit -m "Kali Master: game perkalian PWA"
git branch -M main
git remote add origin https://github.com/USERNAME/kali-master.git
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
const CACHE_NAME = 'kali10-v4';   // ubah menjadi 'kali10-v5', dst.
```

## Testing lokal (opsional)

Service worker hanya aktif lewat `http://localhost` atau `https`, bukan lewat `file://`:

```bash
python -m http.server 8080
# lalu buka http://localhost:8080
```
