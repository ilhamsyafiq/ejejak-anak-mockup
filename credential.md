# CREDENTIAL — e-Jejak Anak (Mockup)

> Akaun demo untuk mockup. Semua kata laluan: **`demo1234`**.
> Data disimpan dalam `localStorage` (bukan pangkalan data sebenar).

---

## 🔑 Akaun Staf — log masuk di `admin-login.html`

> **Peranan & organisasi adalah bebas** — USM boleh ada pentadbir, MAIK boleh ada doktor.

| Peranan | Nama | E-mel | Kata Laluan | Organisasi |
|---|---|---|---|---|
| **Superadmin** | Webimpian (Superadmin) | `superadmin@webimpian.com` | `demo1234` | Webimpian |
| **Pentadbir** | Pn. Salmah Ibrahim | `admin.maik@ejejakanak.my` | `demo1234` | MAIK |
| **Pentadbir** | En. Rosli Abdullah | `admin.usm@ejejakanak.my` | `demo1234` | USM |
| **Doktor** | Dr. Aminah Yusof | `doktor@ejejakanak.my` | `demo1234` | USM |
| **Doktor** | Dr. Zulkifli Hassan | `doktor.maik@ejejakanak.my` | `demo1234` | MAIK |

**Akses ikut peranan (bukan ikut organisasi):**
- **Superadmin**: Statistik · Artikel · Laporan · Profil & Urus Akaun (**semua org**). Tak boleh dipadam.
- **Pentadbir**: Statistik · Artikel · Laporan · Profil & Urus Akaun. Hanya nampak & cipta/padam akaun **dalam organisasinya sendiri** (org dikunci). Tak nampak butiran klinikal anak.
- **Doktor**: Keputusan Saringan · Statistik · Urus Soalan & Domain · Profil. Tak urus akaun.

> Contoh: log masuk `admin.maik@ejejakanak.my` (pentadbir MAIK) → hanya nampak/cipta akaun **MAIK**.
> `admin.usm@ejejakanak.my` (pentadbir USM) → hanya **USM**. Superadmin nampak semua.

---

## 👪 Akaun Ibu Bapa — log masuk di `login.html`

| Nama | E-mel | Kata Laluan | Anak |
|---|---|---|---|
| Siti Nurhaliza | `ibu@contoh.com` | `demo1234` | Aisyah binti Rahman, Haziq bin Rahman |
| Farah Aziz | `farah@contoh.com` | `demo1234` | Nurin Damia |
| Amirul Hakim | `amir@contoh.com` | `demo1234` | Danish Iman |

---

## ℹ️ Nota
- Akaun staf dicipta oleh Pentadbir/Superadmin sahaja (tiada pendaftaran sendiri — AUTH-05).
- Ibu bapa boleh daftar akaun sendiri di `daftar.html`.
- Untuk set semula data demo: jalankan `localStorage.clear()` di konsol pelayar, kemudian muat semula.
- ⚠️ **Kredential ini untuk demo/mockup sahaja** — jangan guna kata laluan lemah ini dalam sistem sebenar.
