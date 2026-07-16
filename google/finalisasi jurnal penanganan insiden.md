## a. sebelumnya...

sebelumnya saya sudah menyelasaikan jurnal penanganan insiden versi awal, sekarang saya akan gunakan setiap bagian untuk mencatat proses, analisis insiden, dan penggunaan tools keamanan.

tidak hanya mencatat apa yang terjadi, namun saya juga coba pahami alurnya. saya akan tulis semua fase dalam siklus kehidupan nist incident response.

---

## b. jurnal 1

| kolom            | keterangan                                                                                                                                                                                                                                             |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| tanggal          | 10 februari 2026                                                                                                                                                                                                                                       |
| nomor            | 1                                                                                                                                                                                                                                                      |
| deskripsi        | analisis insiden ransomware di klinik kesehatan kecil, tercatat kronologi kejadian dengan gunakan metode 5w, serta identifikasi fase deteksi dan analisis dalam siklus respons insiden nist. fokus pada dampak operasional dan penyebab awal serangan. |
| tools            | tidak gunakan tools langsung.                                                                                                                                                                                                                          |
| 5w               | dijelaskan pada bagian penjelasan 5w dibawah table ini.                                                                                                                                                                                                |
| catatan tambahan | karena layanan pasien terganggu, dampak langsung terasa. klinik kemungkinan tidak punya backup offline atau email yang kuat.                                                                                                                           |

### penjelasan 5w

who: peretas terorganisir yang targetkan sektor kesehatan melalui email phising.

what: malware ransomware yang ekripsi sistem dan file rekam medis dan tampilkan catatan tebusan.

when: hari selasa, pukul 09.00 pagi saat jam kerja aktif.

where: jaringan internal klinik kesehatan kecil.

why: karyawan unduh lampiran email phising yang berisi malware ransomware, hingga peretas dapat masuk ke dalam akses sistem.

---

## c. jurnal 2

| kolom            | keterangan                                                                                                                                                                                                     |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| tanggal          | 12 februari 2026                                                                                                                                                                                               |
| nomor            | 2                                                                                                                                                                                                              |
| deskripsi        | investigasi file mencurigakan gunakan tools analisis hash, bagian ini berada pada fase deteksi dan analisis. bertujuan memastikan file termasuk malware berdasarkan nilai hash dan database intelijen ancaman. |
| tools            | virustotal untuk cek hash file dan cek reputasi file melalui database malware.                                                                                                                                 |
| 5w               | tidak digunakan karena bagian ini fokus pada analisis teknis file.                                                                                                                                             |
| catatan tambahan | hash bantu memastikan integritas file, satu nilai hash bisa identifiksi file secara unik. proses ini penting sebelum ambil tindakan lebih lanjut.                                                              |

### penjelasan tools

saya salin nilai hash file mencurigakan lalu upload ke virustotal, hasil menunjukan bahwa file terindikasi malware oleh beberapa engine antivirus. saya paham bahwa analisis hash adalah langkah awal untuk validasi ancaman tanpa menjalankan file secara langsung.

---

## d. jurnal 3

| kolom            | keterangan                                                                                                                                                                                      |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| tanggal          | 14 februari 2026                                                                                                                                                                                |
| nomor            | 3                                                                                                                                                                                               |
| deskripsi        | analisis lalu lintas jaringan gunakan wireshark untuk deteksi aktivitas mencurigakan, bagian ini masuk fase deteksi dan analisis. bertujuan mengidentifikasi pola komunikasi abnormal jaringan. |
| tools            | wireshark untuk capture packet dan analisa protokol.                                                                                                                                            |
| 5w               | tidak digunakan karena bagian ini fokus pada analisis teknis jaringan.                                                                                                                          |
| catatan tambahan | mempelajari cara baca alamat ip sumber dan tujuan serta protokol yang digunakan, saya menemukan koneksi ip eksternal yang tidak dikenal.                                                        |

### penjelasan tools

saya lakukan capture packet jaringan dengan tools wireshark, saya memfilter trafik http dan dns. saya melihat adanya koneksi mencurigakan, aktivitas ini menunjukkan kemungkinan terjadinya komunikasi command and control.

---

## e. jurnal 4

| kolom            | keterangan                                                                                                                                                                          |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| tanggal          | 16 februari 2026                                                                                                                                                                    |
| nomor            | 4                                                                                                                                                                                   |
| deskripsi        | dokumentasi insiden berdasarkan analisis log gunakan konsep siem, bagian gabungkan metode 5w dan masuk dalam fase deteksi dan analisis serta penahanan pada siklus respons insiden. |
| tools            | splunk untuk lakukan query log dan pencarian aktivitas mencurigakan.                                                                                                                |
| 5w               | dijelaskan pada bagian penjelasan 5w dibawah table ini.                                                                                                                             |
| catatan tambahan | log membantu melihat pola login mencurigakan. tanpa log monitoring, aktivitas mencurigakan dapat tidak terdeteksi.                                                                  |
### penjelasan 5w

who: pengguna internal yang akunnya disusupi penyerang.

what: terjadi login tidak biasa dari asal lokasi dan waktu mencurigakan.

when: malam hari di luar jam kerja.

where: sistem autentikasi perusahaan.

why: kemungkinan kredensial bocor akibat phising atau password lemah.

### penjelasan tools

saya gunakan query sederhana melalui splunk untuk mencari login gagal dan login dari ip mencurigakan, hasil tunjukkan anomali pada akun tertentu. saya paham pentingnya tools siem dalam mendeteksi ancaman secara real-time.

---

## f. catatan dan insight pribadi

| kolom   | keterangan                                                                                                                                                                                                                                                                                                                                   |
| ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| catatan | aktivitas paling menantang bagi saya adalah analisis paket jaringan gunakan tools wireshark, banyak sekali data yang muncul dan saya sempat bingung baca pola trafiknya. dengan ini pemahaman saya tentang respons insiden berubah, respons insiden bukan hanya perbaikan sistem yang rusak tapi respons insiden tentang proses terstruktur. |

saya menyadari bahwa keamanan siber bukan hanya soal teknologi canggih, banyak insiden terjadi karena kelalaian kecil seperti terkena phising atau password yang lemah.

saya juga belajar bahwa dokumentasi adalah bagian penting dari pekerjaan analisis keamanan. tanpa catatan jelas, proses investigasi bisa membingungkan.

dengan gunakan beberapa tools keamanan serta mampu dokumentasikan investigasi secara terstruktur, portfolio ini menunjukkan bahwa saya sudah paham tentang dasar deteksi dan respons insiden.