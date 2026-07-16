# automasi dengan python

## a. latar belakang

di skenario ini, saya berperan sebagai seorang professional keamanan di perusahaan layanan kesehatan. saya bertugas perbarui daftar ip address karyawan allow_list.txt yang diizinkan akses catatan pasien. saya buat automasi python untuk hapus ip address berdasarkan remove_list dan tulis ulang file daftar terbaru.

## b. buka file daftar izin

```bash
import_file = "allow_list.txt"

with open(import_file, "r") as file:
    ip_addresses = file.read()
```

nama file disimpan dalam import_file. file dibuka gunakan fungsi open() dengan mode "r" atau read only. pernyataan with pastikan file tertutup otomatis setelah proses selesai.

## c. baca file

```bash
with open(import_file, "r") as file:
    ip_addresses = file.read()
```

metode .read() gunakan untuk baca seluruh isi file jadi satu string yang disimpan dalam ip_address. proses ini tidak ubah isi asli file.

## d. ubah string jadi list

```bash
ip_addresses = ip_addresses.split()
```

metode .split() pisahkan string berdasarkan spasi atau baris baru, ubah ip_address jadi format list supaya setiap ip address dapat diproses secara terpisah.

## e. hapus semua ip address pada remove list

```bash
remove_list = [
    "192.168.97.225",
    "192.168.158.170",
    "192.168.201.40",
    "192.168.58.57"
]

for element in remove_list:
    print(element)
```

perulangan for periksa setiap ip address dalam remove_list. pernyataan if deteksi keberadaan ip address tersebut dalam ip_address, lalu metode .remove() hapus jika menemukan. 

## f. perbarui file

```bash
ip_addresses = "\n".join(ip_addresses)

with open(import_file, "w") as file:
    file.write(ip_addresses)
```

metode .join() gabungkan kembali elemen list jadi string dengan pemisah baris baru (\n). file  dibuka kembali gunakan mode "w" atau write untuk timpa isi lama dengan daftar baru.

## g. ringkasan

automasi ini baca allow_list.txt dan ubah isinya jadi list via .split(), lalu saring ip address yang sudah tidak diizinkan dengan perulangan for dan metode .remove(). terakhir gabungkan kembali via .join() untuk tulis ulang ke file asal gunakan metode mode "w" atau write.