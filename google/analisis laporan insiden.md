# analisis laporan insiden

## a. awal kejadian

pada skenario ini, saya berperan sebagai seorang analis keamanan siber di perusahaan agensi multimedia. perusahaan ini melayani jasa desain website, desain grafis, hingga pemasaran media sosial untuk perusahaan atau bisnis kecil.

suatu hari jaringan internal tiba-tiba tidak bisa diakses, server tidak merespons, dan website klien tidak dapat dibuka. tim menemukan adanya insiden serangan denial of service (dos), yaitu lonjakan paket icmp dalam jumlah yang besar. serangan ini membuat layanan lumpuh selama dua jam.

firewall ternyata tidak dikonfigurasi dengan baik, sehingga penyerang dapat memanfaatkan celah untuk mengirimkan serangan ke dalam jaringan internal. dampak yang diakibatkan insiden ini cukup serius, operasional dapat terhenti, produktivitas menurun, dan  reputasi perusahaan juga berisiko.

saya ditugaskan oleh atasan untuk membuat laporan insiden dan rencana untuk meningkatkan keamanan dengan menggunakan framework nist csf. 

## b. analisis laporan insiden

### tabel analisis

| fungsi       | catatan                                                                                                                                                              |
| ------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ringkasan    | terjadi serangan denial of service (dos) melalui banjir paket icmp, firewall ditemukan tidak terkonfigurasi dengan baik, dan layanan jaringan lumpuh selama dua jam. |
| identifikasi | serangan denial of service (dos) berbasis icmp flood, target adalah jaringan internal dan server layanan, dan celah berasal dari konfigurasi firewall yang lemah.    |
| lindungi     | buat aturan firewall lebih ketat, menerapkan verifikasi ip sumber serta aktifkan ids/ips, dan susun kebijakan hardening firewall.                                    |
| deteksi      | gunakan software monitoring jaringan/siem, terapkan ids/ips untuk deteksi pola trafik abnormal, dan lakukan logging serta analisis trafik secara real time.          |
| tanggapi     | blokir icmp yang masuk, nonaktifkan layanan yang tidak penting, lakukan analisis log firewall, dokumentasikan insiden, dan perbarui konfigurasi keamanan.            |
| pulihkan     | cover/kembalikan layanan yang penting terlebih dahulu, evaluasi sistem yang terdampak, review konfigurasi firewall, dan buat prosedur standar pemulihan.             |

## c. identifikasi (identify)

serangan yang terjadi adalah icmp flood dos, penyerang mengirim ribuan hingga jutaan paket ping ke server. firewall tidak melakukan rate limiting dan tidak ada validasi dari ip spoofing, sehingga paket dapat masuk tanpa penyaringan yang ketat.

sistem yang terdampak:
- server internal
- infrastruktur jaringan
- layanan website klien
- akses internal karyawan

dampak utama:
- downtime selama 2 jam
- gangguan operasional
- potensi kerugian finansial
- penurunan kepercayaan klien

saya menyimpulkan bahwa kontrol preventif belum cukup kuat dan monitoring juga belum optimal.

## d. lindungi (protect)

langkah perbaikan yang dapat dilakukan:
- tambah aturan firewall untuk pembatasan laju icmp
- aktifkan verifikasi ip spoofing
- terapkan ids/ips untuk mendeteksi pola trafik
- gunakan software monitoring jaringan/siem

saya tambahkan rencana perlindungan lanjutan, berupa:
- hardening konfigurasi firewall secara berkala
- audit konfigurasi jaringan internal
- segmentasi jaringan internal
- pelatihan keamanan untuk tim it
- buat dokumentasi standar konfigurasi

alasan penting langkah ini sangat sederhana. firewall adalah pintu gerbang utama, jika pintu tidak dijaga dengan baik maka siapapun dapat masuk.

## e. deteksi (detect)

deteksi menjadi titik yang penting, serangan dos sering terjadi secara tiba-tiba. metode deteksi yang digunakan dan direkomendasikan oleh saya adalah:
- gunakan software monitoring jaringan/siem
- terapkan ids/ips untuk mendeteksi pola trafik abnormal
- analisis log firewall
- aktifkan alert otomatis jika trafik melebihi threshold

tujuan dilakukannya deteksi adalah mempercepat melakukannya tanggapan. semakin cepat diketahui, semakin kecil dampak yang terjadi.

## f. tanggapi (respond)

saat insiden terjadi, ini yang dapat tim lakukan:
- blokir paket icmp yang masuk
- hentikan layanan yang tidak penting
- pulihkan layanan yang krusial

saya menyusun rencana respond untuk di masa depan:
- buat incident response plan yang terdokumentasi
- tentukan peran dan tanggung jawab tim
- simpan log dan bukti untuk keperluan analisis
- lakukan post incident review
- laporkan kepada manajemen dan stakeholder

data yang dibutuhkan untuk analisis:
- log firewall
- log ids/ips
- statistik trafik
- timestamp kejadian
- sumber alamat ip

tanggapan yang baik bukan hanya menghentikan serangan, namun harus menghasilkan perbaikan sistem.

## g. pulihkan (recover)

pemulihan tidak berhenti saat jaringan kembali normal. berikut saya akan menyusun langkah perbaikan:
- validasi konfigurasi firewall baru
- uji stabilitas jaringan
- pastikan tidak ada celah backdoor
- evaluasi performa sistem
- update dokumentasi keamanan
- lakukan simulasi serangan untuk uji ketahanan

informasi yang dibutuhkan saat pemulihan adalah:
- backup konfigurasi
- dokumentasi arsitektur jaringan
- daftar layanan krusial
- prosedur standar pemulihan

saya melihat pentingnya memiliki prosedur tertulis karena tanpa prosedur tertulis, tim yang menangani dapat panik dan membuat kesalahan.

## h. insight pembelajaran

saya belajar bahwa serangan sederhana seperti icmp flood dapat melumpuhkan perusahaan. masalah utama bukan terletak pada kompleksitas serangan, namun terletak pada konfigurasi yang tidak diperhatikan.

framework ini membuat saya berpikir secara sistematis dan tidak mudah untuk panik, berikut saya cantumkan lima fungsi utama nist csf:

| nama         | fungsi                                                 |
| ------------ | ------------------------------------------------------ |
| identifikasi | identifikasi aset, risiko, dan potensi ancaman         |
| lindungi     | perkuat perlindungan dan pertahanan keamanan           |
| deteksi      | percepat proses deteksi teradap aktivitas mencurigakan |
| tanggapi     | tangani insiden secara tepat dan terarah               |
| pulihkan     | pulihkan layanan serta kembalikan stabilitas sistem    |
