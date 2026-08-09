# pengamanan data kesehatan

## a. gambaran project

pada project ini, saya berperan merancang sistem kelola data perusahaan layanan kesehatan bernama securehealth inc. perusahaan simpan data sensitif seperti identitas pasien, tanggal lahir, riwayat medis, informasi asuransi, serta data karyawan.

kondisi ini menyebabkan database perlu pengamanan lebih ketat karena kebocoran data berdampak langsung pada privasi pasien. saya kerjakan pengamanan database dengan mysql dan terapkan kontrol keamanan seperti enkripsi data, rbac, audit log, dan kelola risiko. 

project ini mencakup perancangan arsitektur database, data tata kelola, serta prinsip compliance seperti gdpr dan hipaa.

## b. analisis keamanan

| bagian           | analisis                                                                             |
| ---------------- | ------------------------------------------------------------------------------------ |
| privasi data     | data medis dan informasi asuransi perlu lindungi karena bersifat sensitif            |
| enkripsi         | data sensitif simpan dalam bentuk terenkripsi gunakan aes                            |
| kontrol akses    | akses database dibedakan berdasarkan role doctor, nurse, dan admin                   |
| arsitektur data  | rancang database gunakan relasi antar tabel dan prinsip normalisasi                  |
| tata kelola      | buat aturan mengenai pemilikan, akses, kualitas, dan perubahan data                  |
| manajemen risiko | risiko seperti kebocoran data, akses tidak sah, dan identifikasi kehilangan database |
| kepatuhan        | kontrol keamanan disesuaikan prinsip gdpr dan hipaa                                  |
| audit            | aktivitas dan perubahan data sensitif dicatat lewat logging dan trigger              |

## c. lindungi data

pertama, saya lakukan adalah create database securehealthdb untuk simpan data pasien dan karyawan. beberapa tabel utama digunakan:
- patients
- employees
- roles
- employee_roles

tabel patients simpan informasi sensitif, contoh:
- nama pasien
- tanggal lahir
- riwayat medis
- nomor asuransi

kolom medical_record dan insurance_number dengan tipe varbinary karen data tersebut disimpan dalam bentuk terenkripsi. saya terapkan enkripsi aes pada data sensitif supaya informasi medis dan asuransi tidak disimpan dalam plaintext.

penerapan diberikan lapisan perlindungan tambahan jika seseorang berhasil dapat diakses langsung terhadap database.

## d. role-based access control (rbac)

saya terapkan rbac untuk batasi akses berdasarkan pekerjaan user. role yang digunakan:
- doctor
- nurse
- admin

doctor diberi akses terhadap data yang diperlukan untuk menangani pasien, termasuk data sensitif yang memang diperlukan. nurse diberi akses lebih terbatas dan tidak dapat lihat informasi sensitif. sedangkan admin miliki hak akses lebih luas untuk kelola sistem dan database.

role tersebut disimpan pada tabel roles dan dihubungkan dengan karyawan lewat tabel employee_roles. saya juga create user mysql berdasarkan role tersebut untuk terapkan pembatasan akses secara langsung pada database.

konsep ini diterapkan least privilege, sehingga user tidak dapat akses yang lebih luas dari pada keperluannya.

## e. validasi kontrol akses

setelah rbac diterapkan, saya lakukan pengujian terhadap masing-masing role. skenario pengujian:

| role   | akses                                                                               |
| ------ | ----------------------------------------------------------------------------------- |
| doctor | dapat akses data pasien yang diperlukan termasuk data sensitif                      |
| nurse  | dapat lihat data pasien yang diperlukan, tapi akses terhadap data sensitif dibatasi |
| admin  | dapat miliki akses kelola database yang lebih luas                                  |

uji dilakukan untuk pastikan akses yang diberi benar-benar berjalan sesuai role. saya lihat bahwa rbac tidak hanya digunakan untuk bagi user jadi beberapa kelompok. konfigurasi privilege juga harus diuji supaya tidak over permission.

## f. arsitektur dan tata kelola

saya buat rancangan erd untuk tunjukkan hubungan antara pasien, karyawan, dan role. relasi antara employee dan roles gunakan tabel employee_roles. pendekatan ini membuat satu employee dapat miliki role yang terhubung lewat tabel relasi tanpa simpan data dengan role berulang kali.

struktur database juga dibuat dengan prinsip normalisasi untuk kurangi redundancy dan menjaga konsistensi data. selain arsitektur database, saya susun konsep data tata kelola yang mencakup:
- aturan akses data
- pemilikan data
- kualitas dan kelengkapan data
- keamanan data
- catatan perubahan data
- tanggung jawab role
- kelola data sensitif

pendapat saya, database yang aman tidak cukup hanya miliki konfigurasi teknis. aturan mengenai siapa yang bertanggung jawab data juga harus jelas.

## g. manajemen risiko

saya identifikasi beberapa risiko yang dapat terjadi pada sistem securehealth.

| risiko                 | mitigasi                                    |
| ---------------------- | ------------------------------------------- |
| kebocoran data pasien  | enkripsi data sensitif dan batasi akses     |
| akses user tidak sah   | autentikasi dan rbac                        |
| pencurian password     | simpan password secara aman dan gunakan mfa |
| database terhapus      | backup database secara berkala              |
| ubah data tanpa izin   | kontrol akses dan audit log                 |
| aktivitas mencurigakan | monitoring dan logging                      |
| kegagalan sistem       | backup dan prosedur recovery                |

risiko terbesar skenario ini adalah kebocoran data pasien karena informasi medis dan asuransi adalah termasuk data yang sangat sensitif. kontrol keamanan perlu diterapkan berlapis, satu lapis mekanisme saja tidak cukup jika terjadi kegagalan pada mekanisme lainnya.

## h. kepatuhan dan audit

saya juga terapkan konspe kepatuhan dengan mengacu pada gdpr dan hipaa. beberapa kontrol yang diperhatikan, yaitu:
- batasi akses data pasien
- enkripsi data sensitif
- audit log
- data retention
- monitoring aktivitas pengguna
- kelola hak akses
- perlindungan ubah data tanpa izin

saya aktifkan mysql general query log untuk bantu catat aktivitas query pada database. selain logging, saya gunakan trigger untuk catat perubahan data sensitif seperti informasi pasien.

contoh ketika data pada tabel pasien alami perubahan, aktivitas tersebut dapat dicatat sehingga administrator dapat ketahui perubahan yang terjadi. audit trail bantu proses investigasi ketika temukan aktivitas yang tidak sesuai.

## i. insight pembelajaran

saya belajar, keamanan data kesehatan butuh lebih dari sekadar enkripsi data. akses harus dikontrol berdasarkan role, perubahan data harus dapat dilacak, risiko harus diindentifikasi, dan kelola data harus punya aturan yang jelas.

project ini dapat membuat saya paham tentang hubungan antara keamanan database, kontrol akses, tata kelola data, manajemen risiko, dan kepatuhan.  beberapa konsep yang saya terapkan adalah:

| konsep           | fungsi                                                 |
| ---------------- | ------------------------------------------------------ |
| enkripsi         | lindungi data sensitif                                 |
| rbac             | batasi akses berdasarkan role                          |
| least privilege  | beri akses sesuai keperluan                            |
| tata kelola data | atur kelola dan tanggung jawab data                    |
| manajemen risiko | identifikasi dan kurangi risiko                        |
| audit trail      | catat aktivitas dan perubahan data                     |
| kepatuhan        | pastikan kontrol keamanan mengikuti kebutuhan regulasi |

