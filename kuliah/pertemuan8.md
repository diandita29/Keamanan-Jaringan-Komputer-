Diandita Wira Puspita
1144028
D4 Teknik Informatika 3C
Politeknik Pos Indonesia


ADMINISTRASI JARINGAN KOMPUTER
INSTALASI SNORT PADA SISTEM
OPERASI CentOS




Latar Belakang Snort

Snort adalah open source yang bersedia di berbagai variasi Unix (termasuk Linux) dan juga Microsoft Windows. Snort biasanya disebut sebagai Network Intrusion Detection Sistem (NIDS).

Sebuah NIDS akan memperhatikan seluruh segmen jaringan dimana dia berada, berbeda dengan host based IDS yang hanya memperhatikan sebuah mesin dimana software host based IDS tersebut di pasang. Secara sederhana, sebuah NIDS akan mendeteksi semua serangan yang dapat melalui jaringan komputer (Internet maupun IntraNet) ke jaringan / komputer yang kita miliki.

Sebuah NIDS biasanya digunakan bersamaan dengan firewall, hal ini untuk menjaga supaya snort tidak terancam dari serangan. Sebagai contoh jika snort akan ditempelkan pada interface ISDN ppp0, maka sebaiknya di mesin yang sama di pasang firewall & router  sambungan dial-up-nya. Untuk selanjutnya ada baiknya membaca-baca tentang Firewall-HOWTO atau Firewalling+Masquerading+Diald+dynamic IP-HOWTO, biasa dapat ditemukan di directory /usr/share/doc di Linux.

Teknik Instalasi

Secara umum teknik instalasi snort di Linux sangat mudah. Bagi pemula mungkin ada baiknya menggunakan file RPM yang jauh lebih mudah instalasinya. Pada kesempatan ini saya menggunakan file tar.gz yang sedikit lebih sulit, walaupun sebetulnya tidak terlalu sulit juga. 
Beberapa langkah persiapan yang perlu dilakukan:




Ambil source snort, saya biasanya mengambil source snort yang terakhir langsung dari www.snort.org. Biasanya file source tersebut berbentuk snort-*.tar.gz.
 
Copykan file tar.gz tersebut ke directory /usr/local/src/
 
Buka file snort-*.tar.gz menggunakan perintah # tar zxvf snort-*.tar.gz
 
Biasanya source code snort akan terlihat di folder /usr/local/src/snort-*
 
Pastikan library untuk capture packet (libpcap) terinstall, jika tidak yakin dapat menggunakan software manager melihat apakah libpcap terinstall. Jika belum terinstall install library libpcap tersebut, jika anda menggunakan Mandrake 8.0 hal ini cukup mudah dilakukan karena library tersebut terdapat pada CD Mandrake tsb.
Setelah semua persiapan selesai dilakukan, langkah yang perlu dilakukan untuk menginstalasi tidak banyak, yaitu:
 
Masuk ke directory /usr/local/src/snort-*
cd /usr/local/src/snort-*
 
Konfigurasikan snort menggunakan
./configure
untuk konfigurasi standar praktis tidak perlu di apa-apakan, biasanya pada saat konfigurasi ini kita akan diberitahukan jika ada module yang kurang yang perlu di install, seperti libpcap dll. Usahakan untuk mencari module tersebut di CD distribusi Linux yang kita miliki yang biasanya berbentuk RPM & mudah di install.
 
Selanjutnya mengcompile source code menggunakan
# make
pastikan pada saat di install Linux di konfigurasi untuk melakukan development. Jika Linux tidak di install untuk melakukan development, compiler gcc biasanya tidak terinstall & kita tidak dapat menjalankan perintah make di atas.
 
Setelah source di compile kita menginstall software snort menggunakan
# make install
snort akan di install di directory yang sebenarnya. Default directory tempat instalasi snort adalah /usr/local/bin, /usr/local/man dll. Tentunya kita dapat meletakannya di directory lain selain /usr/local, dengan cara memberikan pilihan –prefix=PATH pada saat melakukan ./configure.

Untuk konfigurasi yang agak aneh-aneh misalnya ingin mengunakan ACID dll, maka kita perlu menambahkan beberapa switch / perintah setelah ./configure, beberapa switch yang mungkin akan digunakan seperti,
 
--with-snmp
menggunakan SNMP alerting code.
 
--with-mysql=DIR
mendukung mysql, perlu di on-kan jika kita menggunakan ACID dengan MySQL.
   
--with-odbc=DIR
mendukung database ODBC, perlu di on-kan jika kita menggunakan ACID dengan database yang tidak ada di daftar.
   
--with-postgresql=DIR
mendukung database Postgresql, perlu di on-kan jika kita menggunakan ACID dengan PostgreSQL.
   
--with-oracle=DIR
mendukung database Oracle, perlu di on-kan jika kita menggunakan ACID dengan Oracle.
 
--with-libpcap-includes=DIR
Jika script konfigurasi gagal memperoleh directory libpcap, maka kita dapat menset secara manual melalui switch ini.
 
--with-libpcap-libraries=DIR
Jika script konfigurasi gagal memperoleh directory libpcap, maka kita dapat menset secara manual melalui switch ini.
 
Setelah selesai di instalasi snort dapat langsung digunakan untuk melakukan sniffing & logging, hanya untuk Network Intrusion Detection System (NIDS) kita perlu melakukan setup / konfigurasi snort. Proses konfigurasi akan sangat ditolong dengan membaca manual SnortUsersManual.pdf yang ada di file snort-*.tar.gz. atau menjalankan perintah ./snort –h


Mengoperasikan Snort

Secara umum snort dapat di operasikan dalam tiga (3) buah mode, yaitu
 
Sniffer mode, untuk melihat paket yang lewat di jaringan.
 
Packet logger mode, untuk mencatat semua paket yang lewat di jaringan untuk di analisa di kemudian hari.
 
Intrusion Detection mode, pada mode ini snort akan berfungsi untuk mendeteksi serangan yang dilakukan melalui jaringan komputer. Untuk menggunakan mode IDS ini di perlukan setup dari berbagai rules / aturan yang akan membedakan sebuah paket normal dengan paket yang membawa  serangan.
Sniffer Mode

Untuk menjalankan snort pada sniffer mode tidaklah sukar, beberapa contoh perintah-nya terdapat di bawah ini,
 
            ./snort –v
            ./snort –vd
            ./snort –vde
            ./snort –v –d –e
 
dengan menambahkan beberapa switch –v, -d, -e akan menghasilkan beberapa keluaran yang berbeda, yaitu
 
            -v, untuk melihat header TCP/IP paket yang lewat.
            -d, untuk melihat isi paket.
            -e, untuk melihat header link layer paket seperti ethernet header.
 
Packet Logger Mode

Tentunya cukup melelahkan untuk melihat paket yang lewat sedemikian cepat di layar terutama jika kita menggunakan ethernet berkecepatan 100Mbps, layar anda akan scrolling dengan cepat sekali susah untuk melihat paket yang di inginkan. Cara paling sederhana untuk mengatasi hal ini adalah menyimpan dulu semua paket yang lewat ke sebuah file untuk di lihat kemudian, sambil santai … Beberapa perintah yang mungkin dapat digunakan untuk mencatat paket yang ada adalah
 
            ./snort –dev –l ./log
            ./snort –dev –l ./log –h 192.168.0.0/24
            ./snort –dev –l ./log –b
 
perintah yang paling penting untuk me-log paket yang lewat adalah
 
            -l ./log
 
yang menentukan bahwa paket yang lewat akan di log / di catat ke file ./log. Beberapa perintah tambahan dapat digunakan seperti –h 192.168.0.0/24 yang menunjukan bahwa yang di catat hanya packet dari host mana saja, dan –b yang memberitahukan agar file yang di log dalam format binary, bukan ASCII.
 
Untuk membaca file log dapat dilakukan dengan menjalankan snort dengan di tambahkan perintah –r nama file log-nya, seperti,
 
            ./snort –dv –r packet.log
            ./snort –dvr packet.log icmp

Intrusion Detection Mode

Mode operasi snort yang paling rumit adalah sebagai pendeteksi penyusup (intrusion detection) di jaringan yang kita gunakan. Ciri khas mode operasi untuk pendeteksi penyusup adaah dengan menambahkan perintah ke snort untuk membaca file konfigurasi –c nama-file-konfigurasi.conf. Isi file konfigurasi ini lumayan banyak, tapi sebagian besar telah di set secara baik dalam contoh snort.conf yang dibawa oleh source snort.
 
Beberapa contoh perintah untuk mengaktifkan snort untuk melakukan pendeteksian penyusup, seperti
 
            ./snort –dev –l ./log –h 192.168.0.0/24 –c snort.conf
            ./snort –d –h 192.168.0.0/24 –l ./log –c snort.conf
 
Untuk melakukan deteksi penyusup secara prinsip snort harus melakukan logging paket yang lewat dapat menggunakan perintah –l nama-file-logging, atau membiarkan snort menggunakan default file logging-nya di directory /var/log/snort. Kemudian menganalisa catatan / logging paket yang ada sesuai dengan isi perintah snort.conf.
 
Ada beberapa tambahan perintah yang akan membuat proses deteksi menjadi lebih effisien, mekanisme pemberitahuan alert di Linux dapat di set dengan perintah –A sebagai berikut,
 
            -A fast, mode alert yang cepat berisi waktu, berita, IP & port tujuan.
            -A full, mode alert dengan informasi lengkap.
            -A unsock, mode alert ke unix socket.
            -A none, mematikan mode alert.
 
Untuk mengirimkan alert ke syslog UNIX kita bisa menambahkan switch –s, seperti tampak pada beberapa contoh di bawah ini.
 
            ./snort –c snort.conf –l ./log –s –h 192.168.0.0/24
            ./snort –c snort.conf –s –h 192.168.0.0/24
 
Untuk mengirimkan alert binary ke workstation windows, dapat digunakan perintah di bawah ini,
 
            ./snort –c snort.conf –b –M WORKSTATIONS
 
Agar snort beroperasi secara langsung setiap kali workstation / server di boot, kita dapat menambahkan ke file /etc/rc.d/rc.local perintah di bawah ini
 
           /usr/local/bin/snort –d –h 192.168.0.0/24 –c /root/snort/snort.conf –A full –s –D
atau
            /usr/local/bin/snort –d –c /root/snort/snort.conf –A full –s –D
 
dimana –D adalah switch yang menset agar snort bekerja sebagai Daemon (bekerja dibelakang layar).

Setup snort.conf

Secara umum ada beberapa hal yang perlu di set pada snort.conf, yaitu:
 
Set konfigurasi dari jaringan kita.
Konfigurasi pemrosesan sebelum di lakukan proses deteksi penyusup.
Konfigurasi output.
Konfigurasi rule untuk melakukan deteksi penyusup.
 
Secara umum kita terutama perlu menset konfigurasi jaringan saja, sedang setting lainnya dapat dibiarkan menggunakan default yang ada. Khususnya konfigurasi rule jika ingin gampang kita ambil saja contoh file *.rules yang ada di snort.tar.gz.
 
Konfigurasi jaringan yang perlu dilakukan sebetulnya tidak banyak, hanya mengisi
 
            var HOME_NET 192.168.0.0/24
 
memberitahukan snort IP jaringan lokal-nya adalah 192.168.0.0/24 (satu kelas C). Sisanya dapat di diamkan saja menggunakan nilai default-nya.
 
Bagian konfigurasi output dapat kita mainkan sedikit untuk menset kemana alert & informasi adanya portscan di kirim, secara default akan dimasukan ke /var/log/snort. Sedikit modifikasi perlu dilakukan jika kita menginginkan untuk menggunakan ACID untuk menganalisa alert yang ada. Output perlu dimasukan ke database, seperti MySQL.
 
Rules biasanya terdapat pada file *.rules. Untuk mengedit sendiri rules agak lumayan, kita membutuhkan pengetahuan yang dalam tentang protokol, payload serangan dll. Untuk pemula sebaiknya menggunakan contoh *.rules yang di sediakan oleh snort yang dapat langsung dipakai melalui perintah include pada snort.conf.

Beberapa contoh rules dari serangan / eksploit dapat dilihat berikut ini,
 
alert tcp $EXTERNAL_NET any -> $HOME_NET 22 (msg:"EXPLOIT ssh CRC32 overflow /bin/sh"; flags:A+; content:"/bin/sh"; reference:bugtraq,2347; reference:cve,CVE-2001-0144; classtype:shellcode-detect; sid:1324; rev:1;)
 
alert tcp $EXTERNAL_NET any -> $HOME_NET 22 (msg:"EXPLOIT ssh CRC32 overflow NOOP"; flags:A+; content:"|90 90 90 90 90 90 90 90 90 90 90 90 90 90 90 90|"; reference:bugtraq,2347; reference:cve,CVE-2001-0144; classtype:shellcode-detect; sid:1326; rev:1;)
 
Cukup pusing bagi pemula, detail berbagai parameter rules terdapat di Snort Users Manual yang juga di sediakan bersama source snort.tar.gz.

Kesimpulan

SNORT adalah salah satu Network IDS dengan 3 mode : sniffer, packet logger dan network instrusion detection. Snort dapat juga dijalankan dibackground sebagai sebuah daemon.

Saran

Bagi pengguna yang memasang snort pada mesin yang sering sekali di serang, ada baiknya memasang ACID, Analysis Console for Intrusion Databases, yang merupakan bagian dari AIR-CERT project. ACID menggunakan PHPlot, sebuah library untuk membuat grafik yang baik di PHP, dan ADODB, sebuah library abstraksi untuk menggabungkan PHP ke berbagai database seperti MySQL dan PostgreSQL.

Scan
https://drive.google.com/open?id=0B17w878LGlWFbVpYX0gtTEgzMkk 
https://drive.google.com/open?id=0B17w878LGlWFTExNMWVFLWktLUk 






