# Chapter 4: Kontrol Proses

## Komponen dalam sebuah proses
Sebuah proses terdiri dari ruang alamat dan serangkaian struktur data dalam kernel. Ruang alamat adalah sekumpulan halaman memori yang telah ditandai oleh kernel untuk digunakan oleh proses. Halaman ini digunakan untuk mentimpan kode, data, dan tumpukan proses. Struktur data dalam kernel melacak status proses, prioritas, parameter penjadwalan, dan lainnya.
Proses dapat dianggap sebagai wadah sumber data yang dikelola oleh kernel atas nama program yang berjalan. Sumber daya ini mencakup halaman memori, deskriptor file, dan atribut lainnya.

Informasi yang dicatat oleh kernel tentang setiap proses meliputi:
1. Peta ruang alamat proses
2. Status proses saat ini (berjalan, tidur, dll.)
3. Prioritas proses
4. Informasi penggunaan sumber data (CPU, memori, dll.)
5. Informasi tentang file dan port jaringan yang dibuka
6. Masker sinyal proses
7. Pemilik proses (ID pengguna yang memulai proses)

### PID: process ID number
Setiap proses diidentifikasi dengan moner PID unik. PID adlah bilangan bulat yang ditetapkan kernel untuk setiap proses saat proses tersebut dibuat. PID digunakan dalam pemanggilan sistem seperti pengiriman sinyal ke proses.

### PPID: parent process ID number
PPID adalah PID dari proses infuk yang membuat proses tersebut. PPID digunakan untuk kerujuk ke proses induk dalam berbagai panggilan sistem, misalnya untuk mengirim sintal ke proses induk.

### UID dan EUID: user ID dan effective user ID
UID adlah ID pengguna yang memilai proses, sedangkan EUID digunakan untuk menentukan hak akses proses ke sumber daya.

## Siklus Hidup Proses
Proses baru dibuat dengan panggilan `fork`. Proses hasil duplikasi memiliki PID yang berbeda, tetapi sebagian besar identik dengan induknya. Sistem Linux menggunakan `clone`, yang merupaakan superset dari `fork`, untuk menangani thread dan fitur tambahan.
Saat sistem boot, kernel membuat beberapa proses, termasuk `init` atau `systemd` yang selalu memiliki PID 1.

### Sinyal
Sinyal digunakan untuk memberi notifikasi pada proses tentang suatu kejaidan,
Jenis sinyal:
- **KILL**: Tidak dapat diblokir, langsung menghentikan proses.
- **INT**: Permintaan untuk menghentikan operasi saat ini (dikirim saat menekan `Ctrl+C`)
- **TERM**: Permintaan untuk menghentikan proses dengan pembersihan sumber daya
- **HUP**: Notifikasi penutupan terminal
- **QUIT**: Mirip dengan TERM, tetapi menghasilkan core dump.

### kill: send sinyal
Perintah `kill` digunakan untuk mengirim sinyal ke proses.
Contoh:
```
kill -9 pid
```

## Monitoring Proesses and Interactive monitoring with top
Perintah `ps` digunaskan untuk memantau proses.
Contoh:
```
ps aux
```
untuk opemantauan interaktif, gunakan `top` atau `htop`

## Nice and renice: changing process priority
Prioritas proses dapat diatur menggunakan perintah `nice` dan diubah menggunakan `renice`.
Contoh:
```
nice -n 10 sh infinite.sh &
renice -n 10 `p 1234
```

## The /proc filesystem
Direktori `/proc` adalah pseudo-filesystem yang digunakan oleh kernel untuk mengekspos informasi tentang status sistem.

## Strace and truss
Gunakan `stace` (Linux) atau `truss` (FreeBSD) untuk melacak pemanggilan sistem dan sinyal.
Contoh:
```
strace -p 5810
```

## Runaway processes

## Periodic processes
Gunakan `cron` atau `systemd timers` utnuk menjalankan tugas berkala
**Format crontab**:
```
* * * * * perintah
```
**Contoh**:
```
30 2 * * * /usr/bin/python3 /path/to/script.py
```
**Perintah systemd**:
```
systemctl list-timers
```

### Penggunaan Umum Tugas yang Terjadwal
- Mengirim email
- Membersihkan filesystem
- Rotasi log
- Menjalankan pekerjaan batch
- Pencadangan dan pencerminan data

Proses kontrol sangan penting untuk mengelolaan sistem operasi berbasis Unix dan Linux, membantu mengelola sumber daya dan menjaga kinerja sistem.
