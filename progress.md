# PROGRESS — e-Jejak Anak (Mockup HTML/JS)

> Fail ini merekod status pembangunan mockup. **Sambung kerja dari bahagian
> "LANGKAH SETERUSNYA" di bawah.** Kemas kini fail ini setiap kali ada perubahan.

Terakhir dikemas kini: sesi pembangunan (27 Julai 2026) — **logo baharu e-Jejak
Anak** (pin+perisai+kanak-kanak) + **re-theme warna MAIK** (merah/emas) + **audit
UX** (skill ui-ux-pro-max: sasaran sentuh 44px, hierarki heading) + **responsif
mobile menyeluruh** + **footer accordion**. Sebelum ini: sistem 4 peranan
(superadmin/admin/doctor/parent), Cetak/PDF keputusan & sejarah, carta trend (Canvas).

---

## 📍 RINGKASAN

Mockup **antara muka sahaja** (HTML + CSS + JS tulen, tiada backend). Semua data
disimulasi dengan `localStorage`/`sessionStorage`. Terletak di:

```
C:\xampp\htdocs\ejejak-anak\mockup\
```
Akses: `http://localhost/ejejak-anak/mockup/`

> ⚠️ Folder `mockup/` berasingan daripada aplikasi Laravel di `ejejak-anak/`.
> ⚠️ Data contoh kini **auto-segar** apabila versi benih naik (kini `ejejak_seed_v3`).
> Sesi benih lama (id `SEED…`) diganti automatik dengan set **6 bulan** untuk carta
> trend; saringan sebenar (id `S…`) dikekalkan. Jika perlu, `localStorage.clear()`.

---

## ✅ SIAP SETAKAT INI

### Struktur & Reka Bentuk
- Template CSS penuh dengan token warna (`assets/css/style.css`) — mudah reskin.
- **Logo e-Jejak Anak** (`assets/img/logo.png`) — pin lokasi merah + perisai emas
  + kanak-kanak melompat. Ganti ikon tapak-kaki lama di header, footer & panel
  admin. `.brand__mark` 56px, `object-fit:contain`; footer diberi lencana putih
  (kontras atas latar merah gelap). Ubah imej: proses semula & bump `?v=`.
- **Skema warna MAIK** (merah `#B31217` + emas `#F4C400`, dari logo Majlis Agama
  Islam Kelantan). Token `:root` ditukar dari teal→merah; teks bahagian gelap
  teal→rose hangat; gradien hero & ikon hero dikemas kini. Kekal: 5 warna domain,
  avatar jantina, warna status (Ya/Belum/Ralat). Semua kontras lulus WCAG AA.
- **Audit UX (skill `ui-ux-pro-max`):** sasaran sentuh min 44×44px (butang/label/
  tab/chip + butang ikon padam) di mobile; hierarki heading dibetulkan (index slide
  2/3 h1→h2, auth aside h2→p, saringan kad h3→h2) — rupa desktop dikekalkan.
- **Footer desktop:** accordion dikawal JS (`syncFooterAcc` dalam `main.js`) — buka
  penuh di desktop, tutup di mobile. `<details open>` lalai + lintas breakpoint 760px.
- **Responsif mobile (3 breakpoint):** 980px (hero/auth/screen-layout jadi 1 lajur),
  760px (menu hamburger, grid → 1 lajur, tab admin leret melintang, kad anak 1 lajur,
  padding seksyen dikurangkan, kaki saringan balut, **footer jadi accordion**), 480px
  (topbar diringkaskan, butang penuh lebar, modal & kad lebih padat, skala fon
  dikecilkan). Semua dalam blok `@media` — paparan desktop tidak berubah langsung.
- **Footer accordion:** 3 kumpulan pautan (Pautan Pantas/Pendidikan/Hubungi) guna
  `<details>/<summary>` — tertutup di mobile (footer paling pendek), sentiasa terbuka
  & toggle dimatikan di desktop (`@media min-width:761px`). Struktur di `buildFooter()`.
- **Cache-busting:** pautan CSS & `<script main.js>` di semua HTML ada `?v=` (kini
  `20260727l`). **Bump nilai ini setiap kali edit style.css / main.js.**
- Header/footer disuntik dari satu sumber (objek `SITE` dalam `main.js`).
- Reka bentuk gaya institusi (rujukan USM-MAIK), logo pin e-Jejak Anak, responsif.
- Header papar status log masuk (nama + Log Keluar) + butang CTA ikut status
  (`data-when="guest|user"`).

### Modul (ikut PDF/spesifikasi)
- **M1 Pendaftaran**: `daftar.html`, `login.html`, `lupa-kata-laluan.html`
  - Pendaftaran kumpul nama, e-mel, **telefon**, kata laluan.
  - Login sahkan akaun sebenar (`ejejak_users`). Demo: `ibu@contoh.com`/`demo1234`.
- **M2 Profil Kanak-kanak**: `dashboard.html` — tambah/padam anak, umur auto.
- **M3 Saringan**: `saringan.html`
  - **Checklist mengikut umur** — soalan ditapis ikut umur anak (julat `minM/maxM`).
  - 5 domain, jawapan Ya/Tidak, kemajuan langsung, banner kumpulan umur.
- **M4 Keputusan**: `keputusan.html` — dicapai/belum, markah domain, mesej nasihat,
  + **maklumat pendidikan** dipapar (ikut Carta Alir).
  - **Cetak / Simpan PDF** (`window.print()` + CSS `@media print`): kepala surat
    USM·MAIK, kromium tapak & butang disembunyikan, warna bar/chip dikekalkan.
- **M5 Pendidikan**: `pendidikan.html` — Artikel/Tips/Aktiviti/FAQ (dipacu data
  `ejejak_articles`, boleh diurus pentadbir).
- **M6 Panel Staf** (`admin.html`, 6 tab — **tapisan mengikut peranan**, lihat bawah):
  1. **Keputusan Saringan** *(doktor)* — triage auto, penapis (cari + Triage + Status),
     **Lihat** (soalan & jawapan), **Hubungi** (Panggilan/WhatsApp/E-mel).
  2. **Statistik Penggunaan** *(semua staf)* — kad ringkasan + **2 carta Canvas**:
     *Trend Saringan Mengikut Bulan* (bar) & *Taburan Triage* (donat + legenda),
     serta purata pencapaian domain. Carta dilukis bila tab dibuka.
  3. **Urus Soalan & Domain** *(doktor)* — tambah/padam soalan (ikut kumpulan umur),
     cipta domain, jadual **liputan soalan mengikut umur**, penapis domain & umur.
  4. **Urus Artikel** *(pentadbir/superadmin)* — CRUD artikel + penapis kategori.
  5. **Laporan Pengguna** *(pentadbir/superadmin)* — jadual + **Muat Turun CSV**.
  5b. **Log Aktiviti** *(pentadbir/superadmin)* — audit demo: catat log masuk,
     cipta/padam akaun, hubungi ibu bapa, eksport, tambah soalan/domain/artikel.
     Pentadbir nampak org sendiri; superadmin nampak semua (`ejejak_audit`).
  6. **Profil & Akaun** — *Profil Saya* (semua staf) + *Urus Akaun Staf*
     (pentadbir/superadmin) **cipta / edit / padam** akaun dengan pilihan peranan
     & organisasi (org dikunci untuk pentadbir).

### Peranan pengguna (4-tier)
**Penting:** `role` (kuasa) & `org` (USM/MAIK) adalah **bebas** — USM & MAIK
kedua-duanya boleh ada pentadbir **dan** doktor. Akses ditentukan oleh peranan.

| Peranan | Boleh lantik | Akses utama | Organisasi |
|---|---|---|---|
| `superadmin` | admin, doktor (semua org) | Statistik, artikel, laporan, urus **semua** akaun (tak boleh dipadam) | Webimpian |
| `admin` (Pentadbir) | admin, doktor (**org sendiri sahaja**) | Urus akaun **dalam org sendiri**, laporan, artikel, statistik. **Tak nampak** butiran klinikal anak | USM / MAIK |
| `doctor` (Doktor) | — | Semak saringan, hubungi ibu bapa, urus soalan/domain, statistik | USM / MAIK |
| `parent` (Ibu Bapa) | — | Daftar, saringan, keputusan sendiri | — |

Tapisan tab: atribut `data-roles` di `admin.html` + `setupRoleAccess()` sembunyikan
tab & sub-panel; fungsi render sensitif (klinikal/laporan) juga disemak peranan.

### Aliran Staf & Data
- Login staf: `admin-login.html` → sahkan `ejejak_admins` (semua peranan staf).
  Kredential penuh lihat `credential.md`. Set contoh **bercampur** (USM ada
  pentadbir, MAIK ada doktor) untuk tunjuk role & org bebas.
- Saringan dihantar → disimpan (`ejejak_submissions`, ada `userId`+`childId`).
- **Log hubungi**: rekod nama doktor + tarikh bila ditandakan "Dihubungi".
- **Sejarah saringan anak**: `sejarah.html?child=…` — senarai sesi lampau + Lihat.
  - **Cetak Sejarah** (seluruh jadual) + **Cetak** satu sesi dari modal (guna
    `#print-region` + `body.print-mode` → laporan penuh markah & jawapan).
  - **Muat Turun PDF** dalam modal *Butiran Keputusan* — jana fail PDF satu sesi
    (`sessionReportPDF()`, bar domain + jawapan, gaya sebaris) guna `html2pdf.js`.
  - **Muat Turun PDF** — muat turun **fail .pdf terus** (satu klik) guna
    `html2pdf.js` (CDN); kandungan sama seperti paparan cetak (kepala surat +
    jadual sesi). Jatuh balik ke dialog cetak jika pustaka gagal dimuat.

### Model Data (localStorage)
| Kunci | Isi |
|-------|-----|
| `ejejak_users` | akaun ibu bapa |
| `ejejak_children` | profil anak |
| `ejejak_admins` | akaun staf (role: superadmin/admin/doctor) |
| `ejejak_domains` | domain + soalan (ada julat umur) |
| `ejejak_articles` | kandungan pendidikan |
| `ejejak_submissions` | keputusan saringan (+ jawapan, log hubungi) |
| `ejejak_audit` | log aktiviti staf (demo audit trail) |
| Sesi: `ejejak_user`, `ejejak_admin` | pengguna log masuk |

---

## 🗂️ FAIL

```
index.html · login.html · daftar.html · lupa-kata-laluan.html
dashboard.html · saringan.html · keputusan.html · sejarah.html
pendidikan.html · admin-login.html · admin.html
assets/css/style.css · assets/js/main.js
README.md · progress.md
```

---

## 🔜 LANGKAH SETERUSNYA (belum dibuat)

Peranan kini **4-tier berasingan** (superadmin/admin/doctor/parent) — lihat
jadual di atas. Cadangan yang BELUM dibina (ikut keutamaan):

1. **Branding USM & MAIK** — papar dua pihak (logo/nama) di header/footer &
   halaman log masuk. (Ditangguh atas permintaan; boleh buat bila-bila.)
2. **Aliran "Lupa Kata Laluan" sebenar** — sekarang halaman ada tetapi tidak
   sambung ke akaun (`ejejak_users`). Perlu jana token mock + set semula.
3. ~~**Cetak / Muat turun PDF keputusan**~~ — ✅ **SIAP** (keputusan & sejarah).
4. ~~**Carta trend statistik**~~ — ✅ **SIAP** (Canvas: trend bulan + donat triage).
5. **Notifikasi mock** — papar pemberitahuan kepada ibu bapa bila doktor hubungi.
6. **Penambahbaikan kecil**: pengesahan borang lebih ketat, keadaan kosong,
   kebolehcapaian (ARIA) untuk modal.

### Idea seni bina masa depan (jika skop berkembang)
- ✅ **SIAP**: peranan Doktor (USM) vs Pentadbir (MAIK) kini berasingan dengan
  privasi berbeza (ADMIN-06: pentadbir tak nampak butiran klinikal anak),
  + Superadmin (Webimpian) untuk bootstrap.
- Bila jadi sistem sebenar: `users.role` perlu tampung `superadmin/admin/doctor/parent`;
  rantaian lantikan — superadmin → admin (boleh lantik admin lain) → doktor.

### 📋 SPEC: Log Audit (demo ringkas SUDAH dibina — tab *Log Aktiviti*)
> **Status:** demo dilaksanakan dalam mockup (`logAudit()` → `ejejak_audit`,
> paparan di tab *Log Aktiviti*). Spesifikasi penuh di bawah ialah untuk **sistem
> sebenar** (jadual DB, IP, append-only sebenar) — mockup hanya tunjuk konsep.

Sistem ini kendalikan data peribadi kanak-kanak & dikongsi 2 agensi (USM/MAIK),
jadi **audit trail wajib** untuk PDPA + akauntabiliti. Rekod tindakan **sensitif**
sahaja (bukan setiap klik).

**Skema cadangan** — jadual `audit_logs`:
| Medan | Keterangan |
|---|---|
| `actor_id`, `actor_role`, `actor_org` | Siapa buat (id, peranan, organisasi) |
| `action` | cth. `login`, `login_failed`, `account.create`, `account.delete`, `role.change`, `screening.view`, `parent.contact`, `question.update`, `report.export` |
| `target_type`, `target_id` | Objek terlibat (cth. `child`, `screening`, `user`) |
| `metadata` (JSON) | Butiran tambahan (cth. medan berubah, format eksport) |
| `ip_address`, `user_agent` | Sumber capaian |
| `created_at` | Cap masa |

**Tindakan minimum untuk dilog:**
1. Auth — log masuk (berjaya/gagal) & log keluar staf.
2. Akaun — cipta / padam / tukar peranan (kritikal: admin boleh lantik admin).
3. Akses data anak — doktor buka keputusan & hubungi ibu bapa *(mockup sudah ada
   log hubungi separa: nama doktor + tarikh)*.
4. Kandungan klinikal — tambah/edit/padam soalan & domain.
5. Eksport — muat turun CSV/PDF laporan (data peribadi keluar sistem).

**Nota akses:** log audit hanya boleh dilihat oleh `superadmin` (dan mungkin
`admin` untuk org sendiri); tak boleh diedit/padam oleh pengguna (append-only).

---

## 🔧 NOTA TEKNIKAL UNTUK SAMBUNG

- Semua logik dalam `assets/js/main.js` (satu fail). Bahagian bernombor:
  ICONS → data layer → seed → header/footer → guard → carousel/tabs/faq →
  auth → dashboard → saringan → keputusan → admin (saringan/domain) →
  **cetak (`printRegion`/`sessionReportHTML`) + carta (`drawBarChart`/`drawDonut`)** →
  stats → laporan/artikel/akaun → sejarah → INIT.
- **Cetak**: `.no-print` sembunyi masa cetak; `.col-action` sembunyikan lajur
  Tindakan; `.print-only` + `.print-head` = kepala surat; `body.print-mode` +
  `#print-region` untuk cetak satu sesi sahaja.
- **Lebar PDF**: kontena laporan `html2pdf` = **700px** (± 185mm) supaya muat
  dalam lebar boleh-cetak A4 (≈718px); lebih lebar akan terpotong di kanan.
- **Muat Turun PDF**: `downloadPDF()` + `historyReportHTML()` guna `html2pdf.js`
  (CDN, dimuat dalam `sejarah.html`) — **satu-satunya pustaka luar**, khusus untuk
  muat turun fail PDF sebenar. Jatuh balik ke `window.print()` jika tak dimuat.
- **Carta**: Canvas tulen (tiada pustaka luar; patuh offline). Dilukis dalam
  `requestAnimationFrame` bila tab Statistik dibuka (canvas perlu lebar tampak).
- Fungsi `init*()` dipanggil dalam `DOMContentLoaded` di hujung fail; setiap satu
  keluar awal jika elemennya tiada pada halaman semasa.
- Kawalan akses: `<body data-auth="parent|admin">` → fungsi `guard()`.
- Semak sintaks: `node --check assets/js/main.js`.
- Data contoh diisi oleh `ensureSeed()` + lazy-seed dalam `getDomains/getArticles/
  getAdmins`.
