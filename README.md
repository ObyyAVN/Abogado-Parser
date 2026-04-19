# Abogado Arch SDK

Parser dan toolkit untuk file script visual novel **Shuumatsu no Sugoshikata ～The World is Drawing to an W/end.～**

---

## Apa Ini?

Abogado Arch SDK adalah kumpulan tool berbasis Python yang dirancang untuk membaca, mengekstrak, dan memodifikasi file script (`.SCF`) dari game visual novel *Shuumatsu no Sugoshikata*. Tool ini cocok digunakan untuk keperluan translation, modding, maupun sekadar menganalisis isi konten game.

File `.SCF` dalam game ini menggunakan encoding **Shift-JIS** dan menyimpan teks dialog, instruksi sistem, serta data menu dalam format biner. SDK ini hadir untuk menjembatani gap antara format biner tersebut dengan teks yang bisa dibaca dan diedit manusia.

---

## Struktur File

Repo ini terdiri dari beberapa file Python dengan peran yang berbeda-beda.

| File | Peran |
|---|---|
| `parser_scf.py` | Parser utama — membaca file `.SCF` dan mengekstrak teksnya |
| `scf_parser_v2.py` | Versi kedua parser dengan penanganan yang lebih baik |
| `injector_scf.py` | Memasukkan kembali teks yang sudah diedit ke dalam file `.SCF` |
| `sdk_tools.py` | Kumpulan utilitas untuk manipulasi file game |
| `sdk_verify.py` | Verifikasi integritas file setelah proses inject |
| `workflow.py` | Mengotomasi seluruh alur kerja dari parse hingga inject |
| `rapihkan.py` | Membersihkan dan merapikan hasil output |

---

## Cara Pakai

Alur kerja utamanya terdiri dari tiga tahap: **parse → edit → inject**.

### Tahap 1 — Parse File SCF

Jalankan parser untuk mengekstrak isi teks dari file `.SCF`:

```bash
python parser_scf.py SCN001.SCF
```

Hasilnya berupa file `.json` atau `.txt` yang berisi dialog dan teks script dari scene tersebut, dalam format yang mudah dibaca.

### Tahap 2 — Edit Teks

Buka file hasil parse (`.json` atau `.txt`) menggunakan text editor apa saja. Lakukan perubahan teks sesuai kebutuhan, misalnya menerjemahkan dialog atau mengganti nama karakter.

### Tahap 3 — Inject Kembali

Setelah selesai mengedit, masukkan kembali teks tersebut ke dalam file `.SCF` asli:

```bash
python injector_scf.py SCN001.json SCN001.SCF
```

File `.SCF` akan diperbarui dengan teks yang baru. Setelah inject, disarankan menjalankan `sdk_verify.py` untuk memastikan integritas file tidak rusak.

### Otomasi dengan Workflow

Jika ingin memproses banyak file sekaligus, gunakan `workflow.py` yang mengotomasi seluruh proses dari awal hingga akhir tanpa perlu menjalankan tiap script secara manual.

---

## Struktur File Game

Untuk referensi, berikut format file yang dikenali oleh SDK ini.

| File Game | Keterangan |
|---|---|
| `SCN***.SCF` | File script per scene (misal `SCN001.SCF`, `SCN002.SCF`) |
| `SCNDAT.TBL` | Tabel data yang memetakan scene ke file script |
| `scene.DSK` / `scene.PFT` | File aset game pendukung |

---

## Requirements

Tool ini membutuhkan **Python 3.x**. Tidak ada dependency eksternal yang wajib, tapi jika ke depannya diperlukan, cukup jalankan:

```bash
pip install -r requirements.txt
```

---

## Sebelum Mulai

Selalu **backup file `.SCF` original** sebelum melakukan proses inject. File yang sudah dimodifikasi tidak bisa dikembalikan secara otomatis, jadi satu salinan backup bisa menyelamatkan banyak pekerjaan.

---

## Disclaimer

SDK ini dibuat semata-mata untuk keperluan edukasi dan penelitian. Pengguna bertanggung jawab penuh untuk memastikan penggunaan tool ini sesuai dengan aturan copyright dan Terms of Service dari game original.

---

## Kontribusi

Pull request dan issue sangat welcome. Untuk perubahan besar, sebaiknya buka issue terlebih dahulu agar bisa didiskusikan sebelum implementasi.
