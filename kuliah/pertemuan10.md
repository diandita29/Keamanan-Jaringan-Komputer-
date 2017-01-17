Diandita Wira Puspita
1144028
D4 Teknik Informatika 3C
Politeknik Pos Indonesia

Sistem Keamanan Jaringan
REMOTE AUTHENTICATION DIAL-IN USER SERVICE (RADIUS)




Pembahasan
RADIUS adalah layanan keamanan untuk otentikasi dan otorisasi pengguna dial-up. Sebuah jaringan perusahaan yang khas mungkin memiliki server akses melekat kolam modem, bersama dengan server RADIUS untuk menyediakan layanan otentikasi. pengguna remote dial ke server akses, dan server akses mengirimkan permintaan otentikasi ke server RADIUS. RADIUS Server mengotentikasi pengguna dan wewenang akses ke sumber daya jaringan internal. pengguna jarak jauh adalah klien ke server akses dan server akses klien ke server RADIUS. RADIUS pada awalnya dikembangkan oleh Livingston Enterprises untuk seri portmaster mereka server akses jaringan. Lucent Technologies membeli Livingston pada Oktober 1997, dan kini mengklaim software itu "diciptakan oleh Access Bisnis Unit Remote dari Lucent Technologies pada tahun 1992." Sisa dari topik ini mengacu pada deskripsi RADIUS disediakan oleh Lucent. Perhatikan bahwa RADIUS merupakan protokol terbuka dan didistribusikan sebagai kode sumber. Hal ini didefinisikan dalam RFC Internet berikut. Lihat "NAS (Network Access Server)" untuk RFC terkait. RFC 2139 (RADIUS Akuntansi, April 1997) RFC 2865 (Remote Authentication Dial Dalam Pengguna Jasa (RADIUS), Juni 2000) Karena RADIUS terbuka, dapat disesuaikan untuk bekerja dengan produk keamanan pihak ketiga atau sistem keamanan proprietary. Server akses yang mendukung protokol client RADIUS dapat berkomunikasi dengan server RADIUS. RADIUS sering disebut sebagai RADIUS AAA, mengacu pada fungsi otentikasi, otorisasi, dan akuntansi. "Akuntansi" mengacu pada kemampuan RADIUS untuk mengumpulkan informasi tentang sesi pengguna yang dapat diolah untuk penagihan dan analisis jaringan. Sistem otentikasi RADIUS dasar menggunakan database pengguna sendiri, tetapi sumber-sumber informasi pengguna termasuk UNIX file password, Sun NIS (Network Information Service), dan direktori yang dapat diakses melalui LDAP (Lightweight Directory Access Protocol). Fitur yang paling penting dari RADIUS adalah model keamanan yang didistribusikan. Pada dasarnya, server komunikasi (akses server atau NAS) terpisah dari server otentikasi. Pendekatan ini lebih terukur dan aman. Informasi akun pengguna disimpan pada server RADIUS pusat yang dapat diakses oleh sejumlah server akses.


RADIUS menggunakan konsep AAA (Authentication, Authorization, Accounting) yaitu :
Authentication
Authentication digunakan untuk membatasi pengguna yang tidak memiliki hak akses agar tidak masuk ke dalam jaringan. Jika pengguna ingin masuk ke jaringan tersebut maka harus diidentifikasi terlebih dahulu agar administrator mengetahui apakah pengguna tersebut memiliki hak akses atau tidak untuk masuk. Metode yang paling umum digunakan untuk mengetahui pengguna yang mengakses jaringan adalah dengan login menggunakan password.

Authorization
Authorization adalah proses lanjutan dari authentication, yaitu memberikan batasan-batasan hak untuk mengakses jaringan, agar pengguna hanya mengakses sesuai hak akses yang dimilikinya. Metode yang paling sering digunakan untuk memberikan pembatasan ini adalah dengan menggunakan atribut yang dirangkai untuk menghasilkan kebijakan tentang hak akses pengguna yang telah disesuaikan dengan informasi yang ada di database.

Kesimpulan 
RADIUS adalah layanan keamanan untuk otentikasi dan otorisasi pengguna dial-up. Sebuah jaringan perusahaan yang khas mungkin memiliki server akses melekat kolam modem, bersama dengan server RADIUS untuk menyediakan layanan otentikasi.

Saran
Sebaiknya mendalami terlebih dahulu mengenai proses radius.

Referensi
http://www.ibm.com/support/knowledgecenter/ssw_i5_54/rzaiy/rzaiyradiusovw.htm 




