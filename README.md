# e-Jejak Anak — Mockup Template (HTML + JS)

Mockup laman web sistem **Saringan Awal Perkembangan Kanak-kanak**.
Dibina dengan **HTML + CSS + JavaScript tulen** (tiada framework, tiada backend)
dan direka sebagai **template** — mudah diubah warna, fon, menu dan kandungan.

> Folder ini **berasingan** daripada aplikasi Laravel di `ejejak-anak/`.
> Ia hanya mockup reka bentuk (antara muka sahaja) untuk rujukan / prototaip.

Reka bentuk mengikut gaya institusi (rujukan: transformasioku.kk.usm.my) —
bersih, profesional, dwi-lapis navigasi, hero carousel, grid kad, footer lengkap.

---

## 🚀 Cara Lihat

Buka dalam pelayar (guna XAMPP, bukan buka fail terus):

```
http://localhost/ejejak-anak/mockup/
```

> Perlu dilayan melalui pelayan (Apache) supaya header/footer yang disuntik
> oleh JavaScript berfungsi. Buka `index.html` terus (file://) juga boleh,
> tetapi lebih baik melalui `localhost`.

---

## 📁 Struktur Fail

```
mockup/
├── index.html              ← Beranda (hero carousel, 5 domain, cara guna)
├── login.html              ← Log masuk ibu bapa
├── daftar.html             ← Pendaftaran akaun
├── lupa-kata-laluan.html   ← Set semula kata laluan
├── dashboard.html          ← Dashboard ibu bapa + profil anak
├── saringan.html           ← Senarai semak (boleh guna TANPA log masuk)
├── keputusan.html          ← Ringkasan keputusan + markah domain
├── pendidikan.html         ← Pusat pendidikan (tab + FAQ)
├── admin-login.html        ← Log masuk DOKTOR / pentadbir
├── admin.html              ← Panel doktor: keputusan diterima + hubungi ibu bapa
└── assets/
    ├── css/style.css       ← SEMUA gaya + token warna (satu tempat)
    └── js/main.js          ← Header/footer, carousel, saringan, panel doktor
```

---

## 🎨 Cara Ubah Template

### 1. Tukar Warna
`assets/css/style.css` → bahagian `:root`. Ubah satu nilai, seluruh laman
bertukar (tiada warna "hardcoded" dalam komponen):

```css
--brand:  #12718A;   /* warna utama   */
--accent: #F4A73F;   /* warna aksen   */
--ok:     #4FA96A;   /* jawapan "Ya"  */
```
Warna 5 domain juga di situ (`--dom-motor-kasar`, dll).

### 2. Tukar Fon
Ubah `--font-head` / `--font-body` dalam `:root`, dan pautan `<link>`
Google Fonts di `<head>` setiap fail HTML.

### 3. Tukar Menu / Footer
`assets/js/main.js` → objek **`SITE`** (menu) dan fungsi `buildFooter()`.
Diedit **sekali sahaja**, terpakai pada semua halaman.

### 4. Tukar Soalan / Domain Saringan
`assets/js/main.js` → tatasusunan **`DEFAULT_DOMAINS`** (seed awal). Setiap soalan
ada julat umur `{ text, minM, maxM }` — **checklist dipaparkan mengikut umur anak**
(Modul 3). Selepas itu, domain disimpan dalam `localStorage` (`ejejak_domains`) dan
doktor boleh **tambah/padam soalan** & **cipta domain baharu** (dengan kumpulan
umur) terus dari panel.

> **Checklist mengikut umur:** saringan hanya papar soalan yang sepadan dengan umur
> anak (cth. 18 bulan → 12 soalan; 42 bulan → 11 soalan berbeza). Doktor pilih
> kumpulan umur semasa menambah soalan.

> **Halaman keputusan** turut memaparkan cadangan Maklumat Pendidikan (mengikut
> Carta Alir "Papar Ringkasan Keputusan & Papar Maklumat Pendidikan").

### 5. Tukar Kandungan Teks
Semua teks berada dalam fail `.html` masing-masing (Bahasa Malaysia).

---

## 👤 Akaun Doktor & Profil

- **Akaun doktor dicipta oleh pentadbir** (AUTH-05) — tiada daftar sendiri. Tab
  **Urus Akaun** dalam panel: cipta/padam akaun doktor (nama, e-mel, telefon,
  jawatan, organisasi **USM/MAIK**), dan kemas kini **Profil Saya**.
- **Log masuk doktor** kini sahkan akaun sebenar (stor `ejejak_admins`).
  Akaun demo: `doktor@ejejakanak.my` / `demo1234`.
- **Log hubungi**: bila doktor tandakan "Sudah Dihubungi", sistem rekod
  **siapa** (nama doktor) & **bila**, dipapar pada jadual & modal.

## 🧒 Sejarah Saringan Anak (ibu bapa)

- Kad anak di dashboard ada butang **Sejarah** → `sejarah.html?child=…`
- Papar semua sesi saringan lampau anak (tarikh, umur, markah, triage) +
  butang **Lihat** untuk melihat markah domain & jawapan setiap soalan (RESULT-06).

## 🔐 Log Masuk, Akaun & Kawalan Akses

- **Saringan memerlukan pendaftaran.** Halaman `dashboard.html`, `saringan.html`
  dan `keputusan.html` dilindungi (`data-auth="parent"`) — pelawat yang belum
  log masuk akan dialihkan ke `login.html`.
- **Header memaparkan status log masuk** — nama pengguna + "Log Keluar" apabila
  telah log masuk (bukan lagi "Log Masuk / Daftar").
- **Akaun demo ibu bapa:** `ibu@contoh.com` / `demo1234` (sudah diisi di borang).
- Pendaftaran mengumpul **nama, e-mel, telefon, kata laluan** — telefon wajib
  supaya doktor boleh menghubungi.

## 🔗 Model Data Selari (User ↔ Admin)

Semua disimpan dalam `localStorage` dan **dikongsi** antara ibu bapa & doktor:

| Kunci | Isi |
|-------|-----|
| `ejejak_users` | akaun ibu bapa berdaftar |
| `ejejak_children` | profil anak (milik user) |
| `ejejak_domains` | domain + soalan (doktor boleh tambah) |
| `ejejak_submissions` | keputusan saringan (ada `userId` + `childId`) |

Setiap saringan yang dihantar merujuk `userId` & `childId` sebenar — jadi data
yang dilihat doktor **selari** dengan akaun & profil anak ibu bapa.

## 👩‍⚕️ Panel Doktor / Pentadbir (Modul 6 — ikut PDF)

Log masuk di `admin-login.html` → `admin.html`. Panel mempunyai **5 tab**:

1. **Keputusan Saringan** (doktor) — semua saringan + **triage automatik**
   (🟢 Pemantauan · 🟡 Perhatian · 🔴 Perlu Rujukan) + **Hubungi ibu bapa**
   (Panggilan / WhatsApp / E-mel dengan mesej pra-isi) + tanda "Dihubungi".
2. **Statistik Penggunaan** *(Modul 6)* — jumlah pendaftaran, profil anak,
   saringan selesai, pengguna aktif, purata pencapaian + purata per domain.
3. **Urus Soalan & Domain** *(Modul 6: Tambah soalan)* — tambah/padam soalan
   pada mana-mana domain, atau cipta domain baharu (nama, warna, ikon, soalan).
4. **Urus Artikel** *(Modul 6: Kemas kini artikel)* — tambah/sunting/terbit/padam
   Artikel, Tips, Aktiviti & FAQ. Perubahan terus dipapar di Pusat Pendidikan.
5. **Laporan Pengguna** *(Modul 6: Jana laporan)* — jadual pengguna +
   **Muat Turun CSV**.

> Kandungan pendidikan kini **dipacu data** (`ejejak_articles`) — apa yang doktor
> ubah di tab "Urus Artikel" terus muncul di `pendidikan.html`.

### Pemetaan Modul PDF → Fail

| Modul (PDF) | Di mana |
|-------------|---------|
| 1 Pendaftaran | `daftar.html`, `login.html`, `lupa-kata-laluan.html` |
| 2 Profil Kanak-kanak | `dashboard.html` (umur auto) |
| 3 Saringan | `saringan.html` (checklist **mengikut umur**, 5 domain, Ya/Tidak) |
| 4 Keputusan | `keputusan.html` (dicapai/belum + ringkasan + maklumat pendidikan) |
| 5 Maklumat Pendidikan | `pendidikan.html` (artikel/tips/aktiviti/FAQ) |
| 6 Pentadbir | `admin.html` (5 tab di atas) |
| Carta Alir | Daftar → Login → Profil → Saringan → Keputusan → Pendidikan |

> Data contoh (3 akaun, 4 anak, 4 saringan, 5 domain, 14 artikel/FAQ) diisi
> automatik pada bukaan pertama. Set semula: `localStorage.clear()` di konsol.

## 🔗 Menyambung ke Laravel (kemudian)

- Salin `assets/css/style.css` & `assets/js/main.js` → `public/` Laravel
- Tukar setiap `.html` → `.blade.php` dalam `resources/views/`
- Ganti stor `localStorage` dengan jadual sebenar mengikut `schema.md`
  (`users`, `children`, `domains`, `questions`, `screenings`)

---

## ⚠️ Nota

Ini **mockup antara muka sahaja** — pengesahan & pangkalan data disimulasi
dengan `localStorage`/`sessionStorage`. Tiada backend sebenar.
