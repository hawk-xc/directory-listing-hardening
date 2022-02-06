# how to prevent Directory Listing bug
Directory listing (dirlisting) adalah sebuah fitur pada web server yang berfungsi menampilkan semua file dalam directory secara otomatis jika ketika file index tidak ada maupun tidak terdeteksi
![Screenshot from 2022-02-03 13-49-20](https://user-images.githubusercontent.com/92193431/152294600-d951b8a6-f62b-4cf9-9425-f62ec07523a1.png)
### bagaimana cara mencegah directory listing pada web server Apache?
Dosis pertama dalam mencegah Directory Listing pada web server APACHE ialah melakukan disable "Options Indexes FollowSymLinks" pada konfigurasi /etc/apache2/apache2.conf"
konfigurasi file apache di " nano /etc/apache2/apache2.conf " lalu lakukan pencarian dengan klik tombol kombinasi "CTRL + w". <br />
<br /><Directory /var/www/><br />
&emsp;        Options Indexes FollowSymLinks <br />
&emsp;        AllowOverride None <br />
&emsp;        Require all granted <br />
<Directory>
<br />
menjadi<br />
```bash
<Directory /var/www/><br />
        Options FollowSymLinks <br />
        AllowOverride None <br />
        Require all granted <br />
<Directory>
```
<br />
hapus options "Indexes" pada FollowSymLinks seperti konfigurasi diatas. yang mengisyaratkan kepada system agar tidak menampilan file jika tidak ada file yang dapat diINDEX.
<br />
### pentest
masuk ke link web server content, disini silakan teman-teman buat index file "index.html" dengan konfigurasi sederhana. jika teman-teman masuk ke link, otomatis web server akan menampilkan index file, atau web content nya. dan sekarang coba teman-teman hapus file index.html, maka secara otomatis web server akan memblokir permintaan dari teman-teman dengan mengirimkan http code 403 (Forbidden).
![Screenshot from 2022-02-03 13-32-17](https://user-images.githubusercontent.com/92193431/152293773-70ec28d0-2395-49ca-a2bf-129cd89ee001.png)
dan jika tidak ada file yang dapat diIndex. <br />
![Screenshot from 2022-02-03 13-43-44](https://user-images.githubusercontent.com/92193431/152294302-a06beea3-1681-4951-907e-fedc96ce8c3b.png)
### summary
jadi itulah cara prevent dari Directory Listing (DirListing), tentunya celah ini berbahaya, dicelah ini hacker dapat dengan mudah mendapatkan Information disclosure pada web server Apache. hacker dapat memanfaatkan celah ini untuk menentukan payload pada file konfigurasi untuk masuk dengan cara mengeksploitasi. ibarat rumah yang pintunya terbuka lebar dan meletakan dokumen penting dibalik pintu 
