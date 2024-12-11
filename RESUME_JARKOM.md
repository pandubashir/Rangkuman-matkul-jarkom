Pandu Bashir Alamin 
20210801155
Rangkuman pertemuan matkul jaringan komputer lanjut

Dimulai dari klasifikasi kelas ip 
Kelas A (0.0.0.0 - 127.255.255.255)
Kelas B (128.0.0.0 - 191.255.255.255)
Kelas C (192.0.0.0 - 223.255.255.255)
Lalu melakukan subnetting yaitu pembagian jaringan misal pada ip (192.168.1.0/24), disini /24 artinya ada 32 - 24 = 8 bit yang tersedia untuk bagian host, Jumlah alamat dalam /24 adalah 256 (total alamat)−2 (dikurangi 2 untuk alamat network dan broadcast) =254host.
•	256 host itu di dapat dari 2 pangkat 8 yang berarti 2×2×2×2×2×2×2×2=256
•	Menagapa 2 pangkat 8 karena Dalam alamat IP, setiap bit bisa bernilai 0 atau 1.
Jika ada 8 bit, maka kita bisa membuat kombinasi 0 dan 1 sebanyak 2 pangkat 8, contoh : 
00000000
00000001
00000010
Pada jaringan /24, ada 8 bit yang tersedia untuk host (bagian terakhir dari alamat IP), contoh : 192.168.0.1/24
Subnet mask digunakan untuk menentukan bagian network dan host dalam alamat IP.
Dalam subnet mask:
-	1 menunjukkan bit yang digunakan untuk network.
-	0 menunjukkan bit yang digunakan untuk host.
Subnet Mask: 255.255.255.0
-	Dalam biner, subnet mask ini terlihat seperti: 11111111.11111111.11111111.0000000011111111.11111111.11111111.0000000011111111.11111111.11111111.00000000
-	Ada 24 bit 1 di awal dan 8 bit 0 di akhir:
-	24 bit pertama untuk bagian network.
-	8 bit terakhir untuk bagian host.
-	
Subnet mask 255.255.255.0 berarti :
- 255 dalam desimal berarti 11111111 dalam biner, yang menunjukkan bit jaringan. 
- 0 dalam desimal berarti 00000000 dalam biner, yang menunjukkan bit host.

Lalu pembahasan tentang routing dynamic dan static 
Routing static adalah metode pengaturan rute jaringan secara manual oleh administrator jaringan. Administrator jaringan mengonfigurasi rute secara langsung di perangkat jaringan (seperti router), menentukan jalur untuk data berdasarkan alamat tujuan. 
Contoh pada WinBox, buka menu IP → Addresses. 
-	Tambahkan IP Address baru, seperti 192.168.10.1/24, dan sesuaikan interface dengan ether yang terhubung ke kabel LAN. Klik Apply dan Ok. 
-	Atur IP di Laptop melalui Control Panel: Masuk ke Network and Internet → Network and Sharing Center → Ethernet → Properties. 
-	Klik dua kali pada IPv4 dan pilih Use the following IP address. Isi dengan 192.168.10.2 (karena 192.168.10.1 sudah digunakan oleh MikroTik). 
-	Tab untuk kolom lain dan klik Ok. Lakukan Ping ke IP Laptop melalui Terminal WinBox.
Kelebihan: 
-	Sederhana dan mudah dikonfigurasi jika jaringan kecil. 
-	Stabil, tidak tergantung pada protokol atau algoritma. 
-	Kontrol penuh atas rute yang digunakan. 
Kekurangan: 
-	Tidak fleksibel: Jika ada perubahan topologi jaringan (misalnya perangkat mati atau jaringan baru ditambahkan), administrator harus memperbarui rute secara manual. 
-	Sulit dikelola: Di jaringan besar, pengelolaan rute statis bisa sangat rumit.
DHCP (Dynamic Host Configuration Protocol) adalah protokol jaringan yang digunakan untuk secara otomatis mengonfigurasi perangkat yang terhubung ke jaringan, seperti komputer, printer, dan perangkat lain, dengan memberikan IP address, subnet mask, default gateway, dan DNS server. Dengan DHCP, perangkat tidak perlu dikonfigurasi secara manual, karena alamat IP dan pengaturan jaringan lainnya diberikan oleh server DHCP secara otomatis.
Selanjutnya untuk mengatur DHCP di MikroTik Router, berikut adalah langkah-langkah yang perlu dilakukan:
1. Menyiapkan IP Address untuk MikroTik
Pastikan MikroTik memiliki IP address yang sesuai dengan jaringan yang akan dikonfigurasi. Misalnya, kita akan mengonfigurasi 192.168.1.0/24 sebagai jaringan lokal.
2. Menambahkan IP Address di MikroTik
•	Masuk ke WinBox atau WebFig.
•	Pilih menu IP → Addresses.
•	Klik + untuk menambahkan alamat IP baru.
•	Masukkan IP yang diinginkan, misalnya 192.168.1.1/24, dan pilih interface (misalnya ether1).
•	Klik Apply dan OK.
3. Mengonfigurasi DHCP Server
•	Pilih menu IP → DHCP Server.
•	Klik DHCP Setup.
•	Pilih interface yang ingin digunakan untuk DHCP (misalnya ether2 untuk jaringan lokal).
•	Klik Next dan MikroTik akan mulai menyiapkan DHCP server.

RIP (Routing Information Protocol) adalah salah satu protokol routing yang digunakan untuk mendistribusikan informasi routing di dalam jaringan. RIP merupakan protokol interior gateway protocol (IGP) yang memungkinkan router-router dalam suatu jaringan untuk saling bertukar informasi mengenai rute yang tersedia, sehingga router dapat menentukan jalur terbaik untuk mengirimkan paket data.
RIP bekerja dengan prinsip distance-vector, yang berarti setiap router mengirimkan informasi tentang jarak (distance) dan arah (vector) ke jaringan tujuan.
Proses Kerja RIP:
1.	Router A mengirimkan informasi routing ke router tetangga setiap 30 detik. Informasi ini mencakup tabel routing yang berisi alamat jaringan yang dapat dijangkau beserta jumlah hop yang diperlukan untuk mencapainya.
2.	Router B menerima informasi dari Router A dan memverifikasi apakah ada rute baru atau perubahan dalam tabel routingnya. Jika ada perubahan, Router B akan memperbarui tabelnya dan mengirimkan informasi baru ke router lainnya.
3.	Proses ini berulang secara berkala, memungkinkan semua router dalam jaringan untuk saling berbagi informasi dan menjaga agar setiap router tahu jalur terbaik menuju tujuan tertentu.

Berikut adalah langkah-langkah sederhana untuk mengonfigurasi RIP pada router MikroTik:
1.	Masuk ke WinBox atau WebFig.
2.	Pilih IP → Routes → RIP.
3.	Aktifkan RIP dengan menambahkan interface yang akan menggunakan RIP.
4.	Atur Network yang akan dipelajari oleh RIP, misalnya:
-	192.168.1.0/24.
5.	Setelah RIP diaktifkan, router akan mulai menerima dan mengirimkan informasi routing ke router lain yang menggunakan RIP.

