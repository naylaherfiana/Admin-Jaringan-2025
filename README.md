# Admin-Jaringan-2025

Tugas 1
1. IP server dan client
   Langkah:
   1. Tulis "http" pada kolom pencarian
   2. Pilih salah satu request
   3. Lihat pada bagian kolom IP sever dan client
   Jawab:
    IP server: 216.239.59.99
    Client: 145.254.160.237

2. Versi HTTP
   Langkah:
   1. Pilih salah satu request HTTP
   2. Buka kolom Hypertext Transfer Protocol
   3. Buka informasi lengkap tentang length info
    Jawab: Request Version: HTTP/1.1

3. Waktu client mengirim request
   Langkah:
   1. Pilih salah satu request HTTP
   2. Buka kolom Frame
   3. Cari time
   Jawab: May 13, 17:17:08 SE Asia Standard Time

4. Waktu server menerima HTTP request dari client
   Langkah:
   1. Pilih HTTP response dari HTTP Request yang tadi dikirim
   2. Buka kolom Frame
   3. Cari time
   Jawab: May 13, 17:17:12 SE Asia Standard Time

5. waktu yang dibutuhkan untuk transfer dan response dari client ke server
   Langkah:
   1. Gunakan Follow TCP Stream untuk melihat alur komunikasi antara client dan server.
   2. Gunakan Delta Time Displayed pada kolom waktu untuk menghitung selisih waktu antara request dan response.
   Jawab: 0.771109s



Tugas 2
Komunikasi data dalam jaingan berdasarkan model lapisan jaringan (OSI atau TCP/IP)
1. Process-to-Process - Transport Layer
   - Lapisan transpost bertanggung jawab untuk komunikasi antar proses di dua perangkat yang berbeda
   - Menggunakan protokol seperti TCP (Transmission Control Protocol) atau UDP (User Datagram Protocol)
   - Pengalamatan port untuk mengidentifikasi aplikasi yang sedang berkomunikasi
2. Host-to-Host - Network Layer
   - Lapisan jaringan bertugas untuk mengirimkan paket data dari satu perangkat ke perangkat lain melalui berbagai jaringan
   - Menggunakan protokol seperti IP (Internet Protocol) untuk menentukan jalur yang harus dilalui data
   - IP address digunakan untuk mengidentifikasi perangkat pengirim dan penerima
3. Node-to-Node - Data Link Layer
   - Lapisan ini menangani komunikasi anatar perangkat dalam satu jaringan fisik
   - Protokol yung digunakan bisa berupa Ethernet, Wi=Fi, atau PPP (Point-toPoint Protocol)
   - Data dikirm dalam bentuk frame, dan MAC address digunakan untuk identifikasi dalam satu jaringan lokal

  Alur Perjalanan Data
  1. Sebuah proses (aplikasi) pada komputer pengirim menginisiasi komunikasi
  2. Data diproses di lapisan transport menggunakan TCP/UDP
  3. Data dikemas menjadi paket IP di lapisan jaringan
  4. Paket dikirim dari satu perangakt jaringan ke perangkat lainnya (router) dalam bentuk frame di lapisan data link
  5. Paket melewati beberapa node (router) di internet, masing-masing melakukan routing ke tujuan akhir
  6. Setelah samapi di host tujuan, data diproses kembali di lapisan transport dan diteruskan ke aplikasi penerima

Tugas 3
Resume Tahapan TCP:L Establishment, Data Transfer, Termination
1. TCP Connection Estasblishment (Three-Way Handshake)
   Membangun koneksi anyara client dan server sebelum data dapat ditransfer
   Step 1: SYN (Synchronize)
   - Client mengirimkan paket SYN ke server untuk memulai koneksi
   Step 2: SYN-ACK (Synchronize Acknowlegde)
   - Server merespons dengan SYN-ACK, menandakan bahwa koneksi diterima
   Step 3:
   - Client mengirimkan ACK untuk mengonfirmasi koneksi berhasil dibangun
   - Setelah ini, koneksi siap untuk mentransfer data
2. TCP Data Transfer
   Setelah koneksi terbentuk, data dapat dikirim antara client dan server menggunakan mekanisme berikut:
   - Segmentation & Reassembly: Data dibagi menjadi segmen-segmen kecil sesuai ukuran maksimum paket (MSS)
   - Numbering & Acknowledgment: Setiap segmen memiliki nomor urut untuk memastikan data diterima dengan benar
   - Flow Control (Sliding Window Protocol): Mengatur jumlah data yang dapat dikirim sebelum mendapatkan ACK
   - Error Handling & Retransmission: Jika data hilang atau rusak, TCP akan meminta pengiriman ulang (retransmission)
3. TCP Connection Termination (Four-Way Handshake)
   Ketika komunikasi selesai, koneksi TCP ditutup melalui proses berikut:
   Step 1: FIN (Finish)
   - Client mengirimkan FIN untuk meminta terminasi koneksi
   Step 2: ACK (Acknowledge)
   - Server mengakui dengan mengirimkan ACK
   Step 3: FIN (Finish)
   - Server mengirimkan FIN untuk menutup koneksi dari sisi server
   Step 4: ACK (Acknowledge)
   - Client mengirimkan ACK sebagai konfirmasi terakhir
   - Setelah ini, koneksi ditutup sepenuhnya
