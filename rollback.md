# ROLLBACK — Panduan Pulih (e-Jejak Anak Mockup)

> Guna fail ini bila **perubahan baharu rosak** dan anda mahu kembali ke keadaan
> yang berfungsi. Semua arahan dijalankan dalam folder `mockup/`.

---

## ⭐ TITIK SELAMAT (checkpoint stabil)

| Tag | Commit | Keterangan |
|-----|--------|------------|
| `stable-v1` | `6394270` | Mockup lengkap, laman live berfungsi (4 peranan, PDF, carta, log audit) |

Laman live: https://ilhamsyafiq.github.io/ejejak-anak-mockup/

---

## 🔖 SEBELUM buat perubahan besar — cipta checkpoint baharu

Supaya senang rollback nanti, tag keadaan yang berfungsi **sebelum** mula kerja besar:

```bash
git tag -a stable-v2 -m "Keterangan keadaan ini"
git push origin stable-v2
```

Lihat semua checkpoint:
```bash
git tag -l
```

---

## 🔙 CARA ROLLBACK (pilih ikut keadaan)

### 1. Belum commit — buang perubahan yang belum disimpan
```bash
git restore .            # buang SEMUA perubahan belum commit
git restore path/fail    # buang perubahan satu fail sahaja
```

### 2. Rollback SATU fail ke titik selamat
```bash
git checkout stable-v1 -- assets/js/main.js
```
(Fail diambil dari checkpoint; commit semula selepas puas hati.)

### 3. Sudah commit tapi BELUM push — undur ke titik selamat
```bash
git reset --hard stable-v1     # ⚠️ buang semua commit selepas stable-v1
```
> ⚠️ `--hard` MEMBUANG perubahan selepas titik itu. Pastikan betul-betul mahu.
> Nak simpan kerja tapi undur commit sahaja: guna `git reset --soft stable-v1`.

### 4. Sudah PUSH ke GitHub — cara SELAMAT (disyorkan): `revert`
`revert` cipta commit baharu yang membatalkan perubahan, tanpa memadam sejarah:
```bash
git revert <hash-commit-yang-rosak>
git push
```
Undur beberapa commit terkini (cth. 3 commit):
```bash
git revert --no-edit HEAD~3..HEAD
git push
```

### 5. Kembalikan SEMUA ke titik selamat, walaupun sudah push (kaedah selamat)
```bash
git revert --no-commit stable-v1..HEAD
git commit -m "Rollback ke stable-v1"
git push
```
Hasil: kandungan sama seperti `stable-v1`, tetapi sejarah dikekalkan.

---

## 🔎 Alat bantu

Lihat sejarah commit (cari titik nak rollback):
```bash
git log --oneline -20
```

Lihat perubahan sesuatu commit:
```bash
git show <hash>
```

Bandingkan keadaan sekarang dengan titik selamat:
```bash
git diff stable-v1
```

---

## ⚠️ ELAK melainkan betul-betul perlu

`git push --force` menulis semula sejarah remote — **berbahaya** kalau orang lain
guna repo. Utamakan **`git revert`** (kaedah 4/5) untuk perubahan yang sudah push.

---

## 📌 Nota

- Data mockup (localStorage) **tidak** disimpan dalam git — rollback kod tidak
  menjejaskan/mengembalikan data pelayar. Untuk set semula data: `localStorage.clear()`.
- Kemas kini jadual **TITIK SELAMAT** di atas setiap kali anda cipta tag baharu.
