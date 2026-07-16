# penilaian kerentanan

## a. titik awal

saya berperan sebagai seorang analis keamanan siber yang baru bekerja di perusahaan ecommerce. perusahaan tersebut menyimpan data pelanggan di server database remote. banyak karyawan bekerja dari berbagai negara, mereka rutin melakukan query untuk menelusuri dan mengelola data.

saya akhirnya menemukan satu hal yang cukup mengkhawatirkan di perusahaan tersebut. ternyata sejak tiga tahun lalu server database tersebut terbuka secara publik, dan siapa pun di internet akan dapat dengan mudah mengakses database tersebut.

saya paham bahwa hal ini bukan risiko yang kecil. database adalah jantung bisnis perusahaan, jika terjadi kebocoran data atau gangguan layanan dapat mengakibatkan dampak yang besar. karena itu saya ditugaskan untuk membuat laporan penilaian kerentanan menggunakan panduan nist sp 800-30 rev. 1.

laporan ini saya susun secara sistematis dengan tujuan bukan hanya menyelesaikan tugas, namun juga untuk  menunjukan kemampuan saya dalam melakukan risk assessment yang terstruktur dan mudah dipahami oleh manajemen lain.

## b. deskripsi sistem

server yang dinilai memiliki spesifikasi berikut:
- sistem operasi: ubuntu server
- database: mysql
- memori: 128 gb
- jaringan: ipv4 publik
- enkripsi koneksi: ssl/tls aktif

secara teknis server ini cukup kuat. jika dilihat permasalahan ini bukan pada spesifikasi hardware maupun software, karena masalah utamanya ada pada kontrol akses pada database tersebut.

permukaan serangan menjadi sangat luas karena:
- port database terbuka
- tidak ada pembatasan ip
- tidak ada segmentasi jaringan
- tidak ada lapisan proteksi tambahan

## c. tujuan penelitian

database memiliki nilai tinggi bagi bisnis, data pelanggan dapat digunakan untuk strategi pemasaran serta melakukan analisis perilaku konsumen. kehilangan data berarti artinya kehilangan aset bisnis.

mengamankan data merupakan tindakan yang sangat penting untuk menjaga kepercayaan pelanggan, kebocoran informasi dapat merusak reputasi perusahaan dan menimbulkan konsekuensi hukum.

server harus selalu tersedia. jika tidak, seluruh karyawan tidak dapat mengakses data dalam database. operasi bisnis akan terdampak langsung dan terganggu, yang akhirnya menimbulkan potensi pendapatan yang menurun.

## d. penilaian risiko

saya akan menggunakan pendekatan kualitatif yang sesuai dengan nist sp 800-30 rev.1, berikut adalah skala yang saya gunakan:

| sumber ancaman | peristiwa ancaman                                                                         | potensi | dampak | nilai risiko |
| -------------- | ----------------------------------------------------------------------------------------- | ------- | ------ | ------------ |
| peretas        | pencurian data pelanggan karena data dapat dijual dan disalahgunakan oleh peretas         | 3       | 3      | 9            |
| pesaing bisnis | pengambilan informasi pelanggan dan internal karena menyangkut masalah rahasia bisnis     | 2       | 3      | 6            |
| orang dalam    | manipulasi dan penyalahgunaan data penting oleh orang dalam yang memiliki niat tidak baik | 2       | 2      | 4            |

## e. pendekatan penilaian

dengan database perusahaan yang terbuka ke publik saya pilih tiga ancaman tersebut, karena fokus saya hanya pada ancaman yang memiliki kombinasi potensi yang tinggi dan dampak yang besar.

penilaian potensi saya ukur berdasarkan exposure sistem hingga ke publik, karena server yang terbuka ke publik memiliki peluang lebih besar untuk diserangan dibandingkan server di jaringan private.

penilaian dampak saya ukur melalui sisi operasional bisnis, reputasi, dan kerugian finansial. jika terjadinya kebocoran data, perusahaan tidak hanya kehilangan data, namun juga kepercayaan pelanggan.

pendekatan ini bersifat kualitatif, penilaian yang saya lakukan berdasarkan kondisi.

## f. strategi remediasi

langkah pertama yang harus dilakukan adalah  penutupan akses database yang terbuka ke publik. server harus dipindahkan ke dalam jaringan server, dan hanya diakses melalui vpn atau lapisan proteksi tambahan.

prinsip least privilege perlu diterapkan, setiap pengguna hanya mendapatkan hak akses yang sesuai dengan kebutuhan pekerjaan. hak akses admin perlu diawasi dan dibatasi.

framework aaa harus digunakan karena banyak kegunaan, contohnya authentication berfungsi memastikan identitas pengguna, sedangkan authorization berfungsi mengatur hak akses, dan untuk accounting berfungsi mencatat seluruh aktivitas.

terapkan defense in depth melalui firewall, lakukan segmentasi jaringan, gunakan proteksi ids/ips, serta lakukan monitoring log secara rutin. backup harian terjadwal juga harus dilakukan untuk menjaga ketersediaan data.

strategi ini menurunkan kemungkinan serangan dan mengurangi dampak jika insiden terjadi.

## g. dampak remediasi

jika kontrol keamanan ini diterapkan:
- turunnya signifikan risiko eksfiltrasi data
- cegah lebih awal akses tidak sah
- terdeteksi aktivitas mencurigakan melalui logging
- stabilkan operasional bisnis

begitupun produktivitas karyawan akan meningkat.

## h. insight pribadi

saya belajar bahwa celah keamanan dengan dampak terbesar bukan karen sistem yang lemah, tetapi masalah sering muncul karena konfigurasi yang kurang tepat.

beresikonya server dengan enkripsi ssl jika aksesnya terbuka secara publik, karena keamanan bukan hanya soal enkripsi. pembatasan akses dan manajemen risiko adalah hal penting bagi keamanan.

penilaian ini melatih saya berpikir dari sisi teknis dan sisi bisnis sekaligus. manajemen lain tidak hanya ingin tahu ada celah, namun ingin tahu juga dampaknya terhadap perusahaan.

porfolio ini menunjukan bahwa saya dapat:
- gunakan standar nist sp 800-30
- lakukan penilaian risiko kualitatif
- hitung tingkat risiko
- usulkan kontrol keamanan yang realistis
- hubungkan risiko dan dampak

saya susun laporan ini secara jujur berdasarkan penilaian logis, dan hasilnya dapat menjadi bahan pembelajaran bagi saya untuk pahami cara melakukan penilaian risiko yang benar.



