## a. kronologi insiden

saya pelajari sebuah kasus insiden keamanan yang terjadi di klinik kesehatan kecil di suatu daerah, insiden tersebut terjadi pada hari selasa jam 09.00 pagi. beberapa komputer dan file rekam medis pasien tidak dapat diakses karyawan.

operasional klinik langsung terganggu, dan tidak dapat gunakan sistem serta muncul catatan tebusan pada layar komputer. peretas minta tebusan sejumlah uang untuk memberikan kunci deskripsi.

saya dokumentasikan kasus ini dengan gunakan incident handler's journal, dengan tujuan melatih kemampuan dokumentasi insident dan paham tentang alur serangan ransomeware secara real.

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

## c. proses analisis

saya membaca skenario dengan detail, saya pisahkan informasi berdasarkan kronologi kejadian. saya mengidentifikasi awal titik masuk serangan yang disebabkan email phising.

lampiran berbahaya berisi malware ransomware di komputer korban, sehingga malware dapat memberi akses ke peretas dan peretas menjalankan ransomware untuk enkripsi file.

saya mencatat bahwa serangan memiliki tahapan yang jelas:
* peretas mengirim email phising kepada korban
* korban unduh file lampiran
* terinstallnya malware di komputer korban
* akses jaringan diperoleh peretas
* ransomeware bekerja di komputer korban
* sistem dan file kemudian terenkripsi
* muncul catatan tebusan minta sejumlah uang

alur ini membantu saya memahami bagaimana satu kesalahan kecil dapat menyebabkan gangguan yang besar.

---

## d. alasan dokumentasi penting

dokumentasi membantu saya untuk berpikir terstruktur. dengan insiden yang tidak mudah dipahami, insiden harus dicatat dengan bertahap.

catatan bisa menjadi referensi jika terjadi kasus serupa. dokumentasi juga penting dalam dunia kerja karena menjadi bukti investigasi.

saya belajar bahwa incident response bukan hanya soal teknis, tetapi komunikasi dan pencatatan juga termasuk bagian yang penting

---

## e. kontrol keamanan

berdasarkan analisis, beberapa kontrol yang seharusnya diterapkan adalah:
- email filtering untuk mendeteksi phising
- endpoint protection atau antivirus
- backup rutin
- segmentasi jaringan
- pelatihan security awareness untuk karyawan
- multi-factor authentication (mfa) untuk sistem penting

ransomeware sering berhasil masuk bukan karena sistem teknisnya yang lemah, namun banyak kasus terjadi disebabkan kurangnya kontrol dasar penting diterapkan.

---

## f. insight pribadi

saya sadar bahwa sektor kesehatan sangat rentan dikarenakan data pasien yang sensitif, serta gangguan sistem bisa berdampak langsung pada pelayanan medis.

serangan terjadi di jam kerja, dampak yang terjadi sangat terasa. operasional klinik berhenti total, situasi ini bisa berbahaya untuk pasien.

saya belajar bahwa manusia adalah titik lemah terbesar dalam keamanan siber, satu klik sembarangan dapat menghentikan seluruh sistem.

jurnal ini dapat membantu saya memahami pentingnya deteksi dini, dan edukasi awareness. saya juga belajar bahwa insiden harus terlihat dari sisi teknis dan dari sisi bisnis.

dokumentasi ini jadi bukti bahwa saya mampu memahami alur serangan ransomeware dan mencatatnya secara terstruktur sesuai dengan praktik incident response dasar.