# audit keamanan internal

## a. kenapa audit ini dilakukan?

pada skenario ini, saya berperan sebagai seorang analis keamanan siber di perusahaan botium toys. perusahaan ini awalnya hanya toko mainan kecil di suatu daerah. satu gedung digunakan untuk kantor, toko, dan gudang.

penjualan online semakin meningkat, pelanggan bukan hanya dari amerika namun dari luar negeri termasuk uni eropa. akibat sistem yang makin kompleks, data pelanggan yang makin banyak, dan pembayaran kartu kredit yang sering diproses mengakibatkan tekanan di dalam tim mulai terasa.

manager it merasa perlu melakukan audit internal, dengan tujuan untuk mengetahui kondisi keamanan saat ini. manager melihat celah dan ingin mengatasinya untuk menghindari kebocoran data, risiko denda, dan menjaga keberlangsungan bisnis.

karena aset yang belum terkelola dengan baik, audit ini dilakukan menggunakan framework nist csf dengan fokus identify. berdasarkan hasil analisis, saya memberikan risk score 8 dari 10 yang artinya masih memiliki potensi risiko yang serius.

## b. tools dan pendekatan yang digunakan

tools audit ini menggunakan:
- framework NIST CSF
- referensi pci dss
- referensi gdpr
- referensi  soc 1 & soc 2
- controls assessment checklist

pendekatan audit dilakukan secara:
- review dokumen
- identifikasi aset
- evaluasi kontrol
- mapping kepatuhan
- analisis gap

## c. aset yang akan diaudit

audit mencakup seluruh program keamanan, berikut adalah aset yang dikelola:
- perangkat on premise
- laptop, komputer, dan smartphone
- sistem ecommerce
- database
- sistem akuntansi dan sistem inventori
- jaringan internal
- internet
- penyimpanan data
- sistem lama (legacy system)
- kamera cctv
- produk di gudang

masalah utama muncul akibat tidak ada manajemen inventaris yang jelas. bahkan semua karyawan bisa mengakses data internal, data kartu kredit dan data pii pelangan.

data kartu kredit juga belum dienkripsi, belum ada ids, belum ada backup data, belum ada disaster recovery plan, kebijakan yang lemah, dan tidak ada manajemen password terpusat.

hanya firewall, antivirus, serta kontrol fisik seperti cctv dan kunci keamanan yang tersedia. 

## d. hasil audit kontrol keamanan

### controls assessment checklist

| ya  | tidak | kontrol                          |
| --- | ----- | -------------------------------- |
|     | x     | least privilege                  |
|     | x     | disaster recovery plan           |
| x   |       | kebijakan kata sandi             |
|     | x     | separation of duty               |
| x   |       | firewall                         |
|     | x     | intrusion detection system (ids) |
|     | x     | pencadangan data                 |
| x   |       | antivirus                        |
| x   |       | enkripsi data                    |
| x   |       | sistem manajemen kata sandi      |

**insight:** 
kontrol teknis sudah ada, walaupun masih dasar. kontrol fisik juga terhitung cukup baik. masalah besarnya ada di kontrol administratif, contohnya tidak menerapkan least privilege, tidak ada separation of duties, dan tidak tersedianya disaster recovery.

letak risiko terbesar ada pada:
- kebocoran data
- penyalahgunaan akses internal
- kehilangan data permanen
- denda dari regulator

## e. hasil audit kepatuhan

### keamanan data kartu pembayaran (pci dss)

| ya  | tidak | praktik terbaik                                                     |
| --- | ----- | ------------------------------------------------------------------- |
|     | x     | hanya pengguna berwenang yang dapat mengakses data kartu kredit     |
|     | x     | data kartu kredit diproses dan disimpan dalam environment yang aman |
|     | x     | terapkan prosedur enkripsi                                          |
|     | x     | terapkan kebijakan manajemen kata sandi yang aman                   |

### perlindungan data uni eropa (gdpr)

| ya  | tidak | praktik terbaik                                         |
| --- | ----- | ------------------------------------------------------- |
| x   |       | jaga kerahasiaan data pelanggan uni eropa               |
| x   |       | terdapat alarm notifikasi 72 jam jika terjadi kebocoran |
|     | x     | data harus dikelompokan dan dikelola dengan benar       |
| x   |       | terapkan kebijakan dan prosedur privasi yang kuat       |

### soc 1 & soc 2

| ya  | tidak | praktik terbaik                                |
| --- | ----- | ---------------------------------------------- |
|     | x     | tetapkan kebijakan akses pengguna              |
|     | x     | jaga data sensitif (pii/spii)                  |
| x   |       | jaga kualitas data akurat dan tervalidasi      |
| x   |       | data hanya tersedia untuk pihak yang berwenang |

## f. hasil analisis dan alasan

berdasarkan analisis, akar masalah yang terjadi ada di manajemen akses dan perlindungan data sensitif. semua karyawan bisa mengakses data internal dan itu melanggar prinsip least privilege, karena dapat mengakibatkan meningkatnya risiko insider threat.

tidak menerapkan enkripsi data, sehingga data kartu kredit dapat terbaca jika terjadi breach. lalu tidak ada backup data dan disaster recovery plan, jika terjadi kena ransomware atau server rusak, operasional bisnis dapat berhenti total.

tidak ada intrusion detection system (ids) dapat mengakibatkan serangan siber tidak terdeteksi. kebijakan password juga masih lemah walaupun ada, sehingga tidak sesuai standar pci dss. begitu juga tidak adanya password manager yang akan mengakibatkan persamaan pasword di banyak sistem.

## g. rekomendasi berdasarkan tingkat risiko

berikut adalah rekomendasi saya yang dapat dilakukan untuk meningkatkan keamanan:

**prioritas tinggi**
- terapkan least privilege
- terapkan separation of duties
- gunakan enkripsi untuk data kartu kredit
- buat disaster recovery plan
- pasang Intrusion detection system (ids)
- terapkan kebijakan password yang lebih complex sesuai standar pci dss
- gunakan manajemen password terpusat

**prioritas menengah**
* buat inventaris aset yang lengkap
* kelompokan data berdasarkan sensitivitas
* buat jadwal monitoring sistem yang jelas
* review ulang akses seluruh karyawan

## h. insight pembelajaran

satu hal penting yang saya pelajari, yaitu banyak perusahaan kecil hingga menengah yang hanya fokus pada penjualan, sedangkan keamanan sering dianggap sepele. risiko denda dari pci dss dan gdpr tergolong sangat besar, reputasi perusahaan pun dapat hancur jika mengalami kebocoran data.

firewall dan antivirus tidak akan cukup, karena keamanan itu adalah kombinasi dari:
* kebijakan
* proses
* teknologi
* manusia

kontrol administratif justru sering diabaikan juga, padahal dapat berdampak besar. dengan dilakukannya audit internal seperti ini membantu melihat kenyataan secara jujur, karena tanpa dilakukannya audit keamanan perusahaan tidak akan sadar dengan kondisi keamanan yang sebenarnya.