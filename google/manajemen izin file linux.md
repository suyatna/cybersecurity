## a. deskripsi proyek

membayangkan saya berperan sebagai professional keamanan yang bekerja bersama tim riset dalam organisasi besar. tugas utama saya adalah pastikan setiap file dan direktori hanya bisa diakses oleh pihak yang tepat.

saya gunakan perintah linux seperti ls -la dan chmod untu periksa serta perbarui izin file, dan hasilnya adalah struktur izin lebih aman dan sesuai dengan kebijakan organisasi.

---

## b. penjelasan string izin 10 karakter

contoh string izin:

```bash
-rw-rw-rw-
```

struktur umum:

```bash
[d/-][rwx][rwx][rwx]
```

penjelasan:

| posisi | karakter | arti                  |
| ------ | -------- | --------------------- |
| 1      | [d]      | file direktori.       |
| 2      | [-]      | file biasa.           |
| 3-5    | [rwx]    | izin user atau owner. |
| 6-8    | [rwx]    | izin group            |
| 9-11   | [rwx]    | izin other            |
penjelasan karakter:
- r = read (baca)
- w = write (tulis)
- x = execute (eksekusi)
- - = tidak miliki izin

contoh -rw-rw-rw- berarti:
- file biasa
- owner bisa read dan write
- group bisa read dan write
- other bisa read dan write

masalahnya kebijakan organisasi tidak izinkan group dan other akses tulis.

---

## c. periksa detail


langkah pertama saya lakukan adalah melihat struktur dan izin file pada direktori proyek. perintah yang saya gunakan:

```bash
researcher2@linux:~/projects$ ls -l
```

output yang didapat:

```bash
total 20
drwx--x--- 2 researcher2 research_team 4096 Jan 19 19:13 drafts
-rw-rw-rw- 1 researcher2 research_team   46 Jan 19 19:13 project_k.txt
-rw-r----- 1 researcher2 research_team   46 Jan 19 19:13 project_m.txt
-rw-rw-r-- 1 researcher2 research_team   46 Jan 19 19:13 project_r.txt
-rw-rw-r-- 1 researcher2 research_team   46 Jan 19 19:13 project_t.txt
```

perintah ls -l tampilkan:
- tipe file
- string izin 10 karakter
- owner
- group
- ukuran
- waktu modifikasi

saya juga gunakan:

```bash
researcher2@linux:~/projects$ ls -la
```

perintah ini tampilkan semua file termasuk file tersembunyi. output tunjukan adanya file tersembunyi:

```bash
total 32
drwxr-xr-x 3 researcher2 research_team 4096 Jan 19 19:13 .
drwxr-xr-x 3 researcher2 research_team 4096 Jan 19 19:35 ..
-rw-rw---- 1 researcher2 research_team   46 Jan 19 19:13 .project_x.txt
drwx--x--- 2 researcher2 research_team 4096 Jan 19 19:13 drafts
-rw-rw-rw- 1 researcher2 research_team   46 Jan 19 19:13 project_k.txt
-rw-r----- 1 researcher2 research_team   46 Jan 19 19:13 project_m.txt
-rw-rw-r-- 1 researcher2 research_team   46 Jan 19 19:13 project_r.txt
-rw-rw-r-- 1 researcher2 research_team   46 Jan 19 19:13 project_t.txt
```

insight yang saya dapat, banyak administrator lupa periksa file tersembunyi. file tersembunyi tetap miliki risiko keamanan jika izinnya salah.

---

## d. kelola file tersembunyi

file .project_x.txt adalah file arsip tim riset, file ini tersembunyi karena diawali titik. kondisi awal:

```bash
total 32
drwxr-xr-x 3 researcher2 research_team 4096 Jan 19 19:13 .
drwxr-xr-x 3 researcher2 research_team 4096 Jan 19 19:35 ..
-rw-rw---- 1 researcher2 research_team   46 Jan 19 19:13 .project_x.txt
drwx--x--- 2 researcher2 research_team 4096 Jan 19 19:13 drafts
-rw-r--r-- 1 researcher2 research_team   46 Jan 19 19:13 project_k.txt
-rw-r----- 1 researcher2 research_team   46 Jan 19 19:13 project_m.txt
-rw-r--r-- 1 researcher2 research_team   46 Jan 19 19:13 project_r.txt
-rw-r--r-- 1 researcher2 research_team   46 Jan 19 19:13 project_t.txt
```

artinya:
- owner = read, write
- group = read, write
- other = tidak ada akses

kebijakan organisasi nyatakan file ini tidak boleh miliki akses write untuk siapapun kecuali owner, group hanya boleh baca. saya jalankan:

```bash
researcher2@linux:~/projects$ chmod g-w .project_x.txt
```

kemudian group pastikan tetap miliki akses baca:

```bash
researcher2@linux:~/projects$ chmod g+r .project_x.txt
```

hasil akhir:

```bash
total 32
drwxr-xr-x 3 researcher2 research_team 4096 Jan 19 19:13 .
drwxr-xr-x 3 researcher2 research_team 4096 Jan 19 19:35 ..
-rw-r--r-- 1 researcher2 research_team   46 Jan 19 19:13 .project_x.txt
drwx--x--- 2 researcher2 research_team 4096 Jan 19 19:13 drafts
-rw-r--r-- 1 researcher2 research_team   46 Jan 19 19:13 project_k.txt
-rw-r----- 1 researcher2 research_team   46 Jan 19 19:13 project_m.txt
-rw-r--r-- 1 researcher2 research_team   46 Jan 19 19:13 project_r.txt
-rw-r--r-- 1 researcher2 research_team   46 Jan 19 19:13 project_t.txt
```

penjelasan penting, file tersembunyi tetap harus taati aturan izin yang sama dan tersembunyi bukan berarti aman.

---

## e. ubah izin direktori

direktori drafts hanya boleh diakses oleh researcher2. kondisi awal:

```bash
total 32
drwxr-xr-x 3 researcher2 research_team 4096 Jan 19 19:13 .
drwxr-xr-x 3 researcher2 research_team 4096 Jan 19 19:35 ..
-rw-r--r-- 1 researcher2 research_team   46 Jan 19 19:13 .project_x.txt
drwx--x--- 2 researcher2 research_team 4096 Jan 19 19:13 drafts
-rw-r--r-- 1 researcher2 research_team   46 Jan 19 19:13 project_k.txt
-rw-r----- 1 researcher2 research_team   46 Jan 19 19:13 project_m.txt
-rw-r--r-- 1 researcher2 research_team   46 Jan 19 19:13 project_r.txt
-rw-r--r-- 1 researcher2 research_team   46 Jan 19 19:13 project_t.txt
```

direktori perlu izin execute untuk bisa akses, saya hapus akses execute dari group dan other:

```bash
researcher2@linux:~/projects$ chmod go-x drafts
```

hasil akhir:

```bash
total 32
drwxr-xr-x 3 researcher2 research_team 4096 Jan 19 19:13 .
drwxr-xr-x 3 researcher2 research_team 4096 Jan 19 19:35 ..
-rw-r--r-- 1 researcher2 research_team   46 Jan 19 19:13 .project_x.txt
drwxr--r-- 2 researcher2 research_team 4096 Jan 19 19:13 drafts
-rw-r--r-- 1 researcher2 research_team   46 Jan 19 19:13 project_k.txt
-rw-r----- 1 researcher2 research_team   46 Jan 19 19:13 project_m.txt
-rw-r--r-- 1 researcher2 research_team   46 Jan 19 19:13 project_r.txt
-rw-r--r-- 1 researcher2 research_team   46 Jan 19 19:13 project_t.txt
```

arti perubahan:
- owner tetap miliki akses penuh
- group dan other tidak bisa masuk direktori

pada izin direktori, execute berarti mampu untuk akses direktori tersebut. tanpa execute, isi direktori tidak bisa diakses walaupun ada read.

---

## f. proses berpikir

saya mulai dari audit izin gunakan ls -la. saya identifikasi file yang miliki write access untuk group atau other, saya sesuaikan izin gunakan chmod.

saya pastikan:
- terapkan least privilege
- tidak ada write access untuk pihak yang tidak sah
- periksa file tersembunyi
- batasi direktori sensitif

keamanan file di linux sangat bergantung pada pengaturan izin yang tepat, kesalahan kecil seperti -rw-rw-rw- bisa buka celah keamanan yang besar.

tools yang digunakan:
- terminal linux
- perintah ls -l
- perintah ls -la
- perintah chmod
- konsep permission string 10 karakter

---

## g. insight pribadi

saya lakukan audit izin file pada direktori proyek tim riset gunakan perintah ls -la, saya identifikasi file yang miliki izin akses yang berlebihan dan memperbaikinya gunakan perintah chmod. saya juga periksa file tersembunyi serta batasi akses direktori sensitif.

pengalaman ini tunjukkan pemahaman saya tentang manajemen izin linux lewat pengetahuan tentang string 10 karakter, serta penerapan prinsip least privilege pada sistem berbasis unix. portfolio ini mereprensentasikan teknis dasar yang penting dalam keamanan sistem dan administrasi linux.