# keamanan akses data

## a. gambaran lab

saya lakukan pengamanan database mysql dengan phpmyadmin dan mysql. di skenario ini, database yang digunakan berisi beberapa tabel saling berhubungan. fokus utamanya adalah atur hak akses user, batasi akses database dan tabel tertentu, serta melindungi data sensitif gunakan enkripsi aes.

pada skenario ini, saya berperan menjadi seorang user dengan role sales_rep yang tidak diberikan akses penuh ke database, karena keperluan akses setiap user harus sesuai dengan tugasnya.

## b. analisa keamanan database

| bagian          | analisis                                                            |
| --------------- | ------------------------------------------------------------------- |
| user management | buat user sales_rep dengan hak akses sesuai kebutuhan               |
| database access | batasi akses user pada database customerorders                      |
| table access    | hapus akses user terhadap tabel tidak diperlukan                    |
| column access   | batasi user hanya dapat ubah kolom tertentu                         |
| encryption      | enkripsi data sensitif gunakan aes                                  |
| key protection  | passphrase tidak gunakan secara langsung, tapi dihash gunakan sha-2 |

kontrol keamanan menerapkan konsep least privilege, yaitu user hanya diberi akses yang diperlukan untuk jalankan tugasnya.

## c. manajemen pengguna (user management)

pertama, saya lakukan yaitu create database customerorders lewat phpmyadmin dan lakukan import database yang sudah disediakan. database berisi beberapa tabel, seperti:
- customers
- employees
- offices
- orders
- payments
- products
- productlines
- orderdetails

setelah database dibuat saya lanjut untuk create user dengan role sales_rep. user tersebut diberi akses:
- select
- insert
- update

pemberian akses dilakukan lewat phpmyadmin di bagian user accounts, saya tidak beri seluruh akses database karena user sales tidak perlu akses penuh seperti administrator.

## d. kontrol akses (access control)

setelah user dibuat saya lakukan pembatasan akses pada database, user sales_rep tidak harusnya dapat akses seluruh informasi perusahaan. beberapa akses tabel, saya lakukan pengaturan lewat menu edit privileges pada phpmmyadmin.

akses terhadap tabel payments dihapus untuk user sales_rep, cara yang sama diterapkan pada tabel:
- employees
- offices

batasan ini penting karena database dapat simpan informasi yang tidak berhubungan dengan pekerjaan user. saya lihat bahwa pemberian akses pada level database masih terlalu luas, pengamanan juga perlu dilakukan hingga level tabel dan kolom.

## e. akses level kolom

salah satu bagian menarik adalah pembatasan akses hingga level kolom. di tabel customers, user sales_rep tetap diberi akses terhadap tabel, tapi tidak semua kolom diubah. kolom creditlimit jadi pengecualian karena user masih perlu lakukan update terhadap kolom creditlimit, sedangkan kolom lainnya tidak diberikan akses update.

kolom lainnya tidak diberi permission update, konsep dibuat aksesnya lebih spesifik. user tidak dibatasi berdasarkan tabel, tapi juga berdasarkan data yang boleh diedit. saya juga lakukan praktik yang sama di tabel products, dengan batasi user supaya tidak dapat lakukan update di kolom buyprice. hal tersebut ditunjukkan bahwa access control diterapkan lebih detail.
## f. lakukan enkripsi (encryption)

selanjutnya, saya amankan data sensitif dengan enkripsi. saya gunakan aes untuk enkripsi data database. sebelum lakukan enkripsi, passphrase tidak langsung gunakan sebagai key, saya lakukan hashing gunakan sha-2 dengan panjang 512 bit.

contoh key:

```bash
SET @key_str = SHA2('My secret passphrase', 512);
```

database dipilih gunakan:

```bash
USE customerorders;
```

saya lakukan pengecekan data pada tabel customers sebelum enkripsi.

```bash
SELECT * FROM customers LIMIT 5;
```

kolom addressline1 kemudian ubah menjadi tipe varbinary karena hasil enkripsi aes berupa data binary.

```bash
ALTER TABLE customers MODIFY COLUMN addressLine1 VARBINARY(255);
```

data enkripsi gunakan:

```bash
UPDATE customers
SET addressLine1 = AES_ENCRYPT(addressLine1, @key_str);
```

setelah proses tersebut selesai, data pada addressline1 tidak lagi simpan dalam bentuk plaintext.

## g. lakukan dekripsi (decryption)

enkripsi dibuat untuk data tidak dapat dibaca langsung, data tetap harus dapat dikembalikan ketika user yang miliki hak akses memang diperlukan. saya gunakan perintah berikut untuk baca kembali data:

```bash
SELECT CAST(
	AES_DECRYPT(addressLine1, @key_str)
	AS CHAR(255)
)
FROM customers;
```

hasil tunjuk bahwa data dapat dikembalikan ke bentuk semula, selama key digunakan sesuai. praktik ini tunjukkan bahwa enkripsi tidak hanya ubah data menjadi ciphertext. kelola key juga penting karena kehilangan key dapat disebabkan data tidak dapat dienkripsi.
## h. insight pembelajaran

saya belajar bahwa keamanan database tidak cukup gunakan username dan password. akses user dibatasi didasari kebutuhan. privilege terlalu luas dapat tingkatkan risiko ketika akun berhasil digunakan oleh pihak yang tidak seharusnya.

terapan least privilege dibuat untuk akses jadi lebih terkontrol, pembatasan dapat dilakukan di level database, tabel, serta kolom. enkripsi jadi alasan keamanan tambahan ketika database simpan informasi sensitif. data tersimpan dalam plaintext memiliki risiko lebih besar jika dapat diakses oleh pihak yang salah.

lab dibuat untuk saya pahami tiga bagian penting dalam database security:

| konsep             | fungsi                                                            |
| ------------------ | ----------------------------------------------------------------- |
| manajemen pengguna | atur akun yang dapat akses database                               |
| kontrol akses      | batasi database, tabel, serta kolom yang dapat digunakan pengguna |
| enkripsi           | lindungi data sensitif supaya tidak tersimpan dalam plaintext     |
