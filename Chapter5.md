# Chapter 5: Sistem File
Tujuan dasar sistem berkas adalah untuk mewakili dan mengatur sumber data penyimpanan sistem.
Sistem berkas dapat dianggap terdiri dari 4 komponen utama:
1. Namespace - cara memberi nama sesuatu dan mengaturnya dalam hierarki
2. API - sekumpulan sistem penggilan untuk menavigasi dan memanipulasi objek
3. Model keamanan - skema untuk melindungi, menyembunyikan, dan berbagi objek
4. Implementasi - perangkat lunak untuk menghubungkan model logis dengan perangkat keras.

Sistem berkas berbasis disk yang dominan adalha ext4, XFS, dan UFS, serta ZFS dari Oracle dan Btrs. Ada juga sisyem berkas lain seperti VxS dari Veritas dan JFS dari IBM.
Selain itu, ada sisyem berkas asing seperti FAT dan NTFS yang digunakan oleh Windows serta sistem berkas ISO 9600 yang digunakan oleh CD dan DVD.
Sebagian besar sistem berkas modern berusaha mengimplementasikan fungsionalitas isyeom berkas taradisional dengan cra uang lebih cepat dan andal, atau menambaahkan fitur tambahan di atas semantik sisyem berkas standar.

## Pathname
Istilah "folder" berasal dari Windows dan macOS. Secara teknis, ia memiliki arti yang sama dengan "direktori". Jangan gunakan dalam konteks teknis.
Daftar direktori yang mengarah ke suatu file disebut pathmane. Pathname adalah string yang menggambarkan lokasi file dalam hierarti sisyem berkas. Pathname dapat bersifat absolut (misalnya, `/home/username/file.txt`) atau relatif (misalnya, `/file.txt`).

## Mounting dan Unmounting Sistem Berkas
Sistem berkas terdiri dari bagian-baigan kecil, juga disebut "sistem berkas", yang masing-masing terdiri dari satu direktori beserta subdirektori dan berkasnya.Istilah "pohon berkas" digunakan untuk merujuk pada tata letak keseluruhan, sementara "sistem berkas" merujuk pada cabang-cabang yang terpasang pada pohon.
Dalam banyak kasus, sistem berkas dipasang ke pohon mengguankan perintah `mount`. Perintah ini memetakan direktori dalam phon berkas yang sudah ada (disebut titik pemasangan) ke root dari sistem berkas baru.
Contoh:
```
# Memasang sistem berkes pada /dev/sda4 ke /users
mount /dev/sda4 /users
```
Linux memiliki opsi unmount singkat (`umount -l`) yang menghapus sistem berkas dari hierarki penamaan tetapi tidak benar-benar mencopotnya sammpai tidak lagi digunakan.
Perintah `umount -f` digunakan untuk pemaksaan unmount, berguna saat sistem berkas sedang sibuk.
Sebagai alternatif, gunakan `lsof` atau `fuser` untuk mencari tahu proses mana yang mengguanakn sistem berkas dan tutup proses tersebut sebelum melakukan unmount.

## Organisasi file tree
Sistem UNIX tidak pernah terorganisir dengan baik, beberapa konvensi penamaan yang tiddak ko,patibel digunakan secara bersamaan, dan jenis berkas yang berbeda tersebar secara acak dalam namespace. Inilah sebabnya mengapa sulit untuk meningkatkan sistem operasi.
Sistem berkas root mencakup setidaknya direktori root dan sekumpulan file serta subdirektori minimal. Kernel OS biasanya berada di bawah `/boot`, tetapi lokasi pastinya bisa bervariasi.
- `/etc` berisi file sistem dan konfigutasi kritis
- `/sbin` dan `/bin` untuk utilitas penting
- `/tmp` untuk file sementara
- `/dev` awalnya bagian dari sistem berkas root, tetapi kini biasanya merupakan sistem berkas virtual yang dipasang secara terpisah
- `/usr` menyimpan program standar yang tidak bersifat kritis terhadap sistem
- `/var` menyimpan direktori spool, file log, informasi akuntansi, dan berbagai item lain yang tumbuh atau berubah dengan cepat.

## Jenis File
Sebagian besar implementasi sistem berkas mendefinisikan tujuh jenis file:
1. Berkas reguler
2. Direktori
3. Berkas perangkat karakter
4. Berkas perangkat blok
5. Soket domain lokal
6. Pipa bernama (FIFO)
7. Tautan simbolik
Untuk menentukan jenis suatu file, gunakan perintah `file` atau `ls -ld`

## Hak Akses File
Dalam model sistem berkas Unix/Linux, setiap file memiliki sembilan bit izin yang menentukan siapa yang dapat membaca, menulis, dan mengeksekusi file tersebut. Ditambah tiga bit lainnya yang terutama mempengaruhi eksekusi program.
Setiap file memiliki:
- Pemilik (`u`)
- Grup (`g`)
- Lainnya (`o`)

Gunakan perintah chmod untuk mengubah izin file.
Contoh:
```
chmod u+w file.txt  # Menambahkan izin tulis untuk pemilik file
chmod 755 script.sh # Izin eksekusi untuk semua orang, hanya pemilik yang bisa menulis
```
### Perintah Terkait File
- `ls -l`: Melihat informasi file
- `chmod`: Mengubah izin file
- `chown`: Mengubah kepemilikan file
- `chgrp`: Mengubah grup file
- `umask`: Menentukan izin default untuk file baru

### Daftar Kontrol Akses (ACL)
Model izin Unix tradisional sederhana dan efektif tetapi memiliki keterbatasan. ACL digunakan untuk memperluas model ini, memungkinkan file memiliki banyak pemilik dan memberikan izin berbeda kepada berbagai pengguna.
Gunakan `getfacl` dan `setfacl` untuk melihat serta mengatur ACL pada file.
Contoh:
```
getfacl /etc/passwd
setfacl -m u:abdou:rw /etc/passwd
```
