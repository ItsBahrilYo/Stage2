# Hi There! Welcome 
# Selasa
Kali ini saya akan menjelaskan tentang cloud computing menggunakan idcloudhost, managed database dan setup backend sederhana 

## Cloud Computing dengan IDCH
<p>Cloud computing merupakan teknologi memvirtualisasi resource berupa server yang dimana kita bisa mendapatkan aksesnya dan mengkostumisasi system requirementnya (core, memory, disk) melalui jaringan.

IDCH (idcloudhost) merupakan suatu web hosting provider yang ada di Indonesia yang menawarkan layanan seperti pendaftaran domain, cloud hosting, server (VPS & Dedicated Server) dan masih banyak lagi</p>
___
 ### 1. Membuat VM untuk Aplikasi di idcloudhost dan Setting SSH
  
  * Pergi ke website idcloudhost.com lalu login di bagian console

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/1-Build-VM-dan-SettingSSH-/1.png?raw=true)

* Setelah login sebenarnya bisa langsung membuat vm pada menu create virtual machine di dasboard utama, namun kali ini saya menggunakan akun dumbways yang sudah mengirim invitation ke saya untuk membuat vm di akun dumbways

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/1-Build-VM-dan-SettingSSH-/5.png?raw=true)

* Setelah masuk lalu scroll sedikit ke bawah, akan terlihat menu virtual machine compute, lalu klik menu tersebut

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/1-Build-VM-dan-SettingSSH-/7.png?raw=true)

* Pada bagian ini kita akan mengkostumisasi type resource, os, lokasi data centernya, size (core, mem, disk), lalu klik create
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/1-Build-VM-dan-SettingSSH-/8.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/1-Build-VM-dan-SettingSSH-/9.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/1-Build-VM-dan-SettingSSH-/10.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/1-Build-VM-dan-SettingSSH-/11.png?raw=true)

* VM sedang di build
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/1-Build-VM-dan-SettingSSH-/14.png?raw=true)

* Setelah proses build VM selesai kita bisa lihat spesifikasi VM di sebelah kanan

* Lalu dari sini kita akan remote VM-nya dengan SSH, copy ip public dari VM tersebut
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/1-Build-VM-dan-SettingSSH-/16.png?raw=true)

* Pergi ke terminal dan masukkan command remote SSH nya
dan paste ip public setelah command berikut

```bash
  ssh bahril@103.183.74.115
```

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/1-Build-VM-dan-SettingSSH-/17.png?raw=true)


* Done, kita sudah masuk ke dalam VM yang kita buat
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/1-Build-VM-dan-SettingSSH-/18.png?raw=true)

* Sepeti yang kita lihat di langkah sebelumnya, kita masuk ke VM, VM akan meminta password, kita akan hiangkan step meminta password ini dengan ssh-keygen, atau bisa di bilang kita memberi kunci pada VM kita

```bash
  ssh-keygen
```

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/1-Build-VM-dan-SettingSSH-/19.png?raw=true)

* Lalu pergi ke .ssh/ , dan didalam file tersebut ada 3 buah file , tampilkan file id_rsa (private key) lalu copy isi dari file tersebut

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/1-Build-VM-dan-SettingSSH-/22.png?raw=true)

* Pergi ke terminal lokal dan buat directory dan file untuk menyimpan private key dari VM tadi

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/1-Build-VM-dan-SettingSSH-/23.png?raw=true)

* Paste private key tadi kedalam file yang dibuat tadi disini saya namai filenya bahrilkey, lalu save dan exit

* file ini nantinya akan berfungsi sebagai penampung private key dari beberapa VM yang kalian buat yang nantinya akan digunakan untuk masuk ke setiap VM tanpa menggunakan password

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/1-Build-VM-dan-SettingSSH-/24.png?raw=true)

* Lalu atur permission filenya menjadi 400 agar group dan other tidak bisa red,write dan execute file kunci tersebut
```bash
  chmode 400 bahrilkey
```

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/1-Build-VM-dan-SettingSSH-/25.png?raw=true)

* Lalu masuk ke dalam VM dengan menggunakan key yang sudah dibuat

```bash
  ssh -i bahrilkey bahril@103.183.74.115
```
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/1-Build-VM-dan-SettingSSH-/26.png?raw=true)

___

### 2. Buat VM untuk WebServer NGINX di idcloudhost

* Kali ini kita akan membuat satu server lagi untuk web server

* Masuk pada menu create new resource, kustomisasi dengan spesifikasi seperti di gambar

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/2-Build-VM-NGINX/1.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/2-Build-VM-NGINX/2.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/2-Build-VM-NGINX/3.png?raw=true)

* Server untuk web server sudah berhasil dibuat

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/2-Build-VM-NGINX/4.png?raw=true)

* Pada server aplikasi sebelumnya kita setting ssh-key agar bisa masuk ke server tanpa password tapi menggunakan publickey yang tertampung di file authorize key. Kini kita akan copy directory .ssh/ dari server aplikasi dan paste ke .ssh/ di server web server

```bash
  scp -r .ssh bahril@103.176.76.168:/home/bahril/.ssh/
```

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/2-Build-VM-NGINX/7.png?raw=true)

* Install nginx di webserver dan test running

```bash
  sudo apt install nginx
```
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/2-Build-VM-NGINX/9.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/2-Build-VM-NGINX/10.png?raw=true)

___

### 3. Pengaturan SSH key

* Disini kita akan mengintegrasikan kedua server (server aplikasi dan web server) dengan lokal kita menggunakan publickey dan private key

* Private key disini alangkah baiknya jika hanya terintegrasi  pada lokal kita, tepatnya pada folder dan file yang telah kita buat sebagai tempat penampung private key tadi. Mengapa demikian? Karena misalkan private key dari server developer A ada di server developer B besar potensi kalau terjadi duplikasi code, pencurian code dan hal-hal berbahaya lainnya. Kasus lain lagi misal privatekey lokal kita ada di salah satu server developer, maka developer trsebut bisa leluasa masuk kedalam lokal kita dan potensi hal buruk menjadi meningkat.

* Public key akan sangat berguna ketika seorang developer yang telah mempunyai akses server aplikasinya ingin melakukan checking apakah datanya sudah termigrasi di webserver yaitu dengan memasukkan publickey webserver kedalam file authorizekey yang ada di .ssh/ dari server developer.


* Copy publickey di server aplikasi ke dalam file authorized_keys

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/3-Pengaturan-SSHkey/1-disvr-app.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/3-Pengaturan-SSHkey/2disvr-app.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/3-Pengaturan-SSHkey/3-disvr-app.png?raw=true)


* Selanjutnya kita akan mengintegrasikan private key masing-masing VM kedalam lokal kita.

* Copy semua tulisan yang ada didalam id_rsa dari masing-masing VM lalu paste kedalam file key yang sudah dibuat

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/3-Pengaturan-SSHkey/pembuatan-bahrilkey-1.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/3-Pengaturan-SSHkey/pembuatan-bahrilkey-2.png?raw=true)


* Masukkan publickey dari masing-masing VM kedalam authorized_keys yang ada di .ssh masing-masing VM lalu copy juga publickey satu VM dan paste ke authorized_keys VM lain

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/3-Pengaturan-SSHkey/publickey-diappserver.png?raw=true)


![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/3-Pengaturan-SSHkey/publickey-diwebserver.png?raw=true)

___
### 4. Setting Reverse Proxy di Web Server

* Membuat directory untuk file reverse proxynya yaitu di /etc/nginx/. Lalu ubah kepemilikan agar user 'bahril' dapat mengubah file yang ada didalam directory yang dibuat dengan command

```bash
  sudo chown bahril:bahril dumbflix
```

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/5-reverseproxy/2.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/5-reverseproxy/3.png?raw=true)

* Lalu buat file reverse proxynya 
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/5-reverseproxy/4.png?raw=true)

* Isi file tersebut dengan code dibawah ini 

```bash
  server { 
    server_name <nama domain>; 
    
    location / { 
             proxy_pass http://<ip server aplikasi>:3000;
    }
}
```
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/5-reverseproxy/5.png?raw=true)

* Lalu kembali ke directory /etc/nginx/ lalu edit file nginx.conf. Setelah masuk ke text editor lalu scroll ke bawah hingga menemukan tulisan include lalu masukkan directory file reverse proxy yang dibuat tadi

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/5-reverseproxy/6.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/5-reverseproxy/7.png?raw=true)


___

### 5. Deploy Aplikasi Fronntend

* Pergi ke dalam server aplikasi dan clone project terlebih dahulu

```bash
  git clone <url project>
```
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/4-nvm-npm-pm2-diserverapps/2.png?raw=true)

* Install nvm 
```bash
  curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
```
```bash
  exec bash
```
```bash
  nvm i 14
```
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/4-nvm-npm-pm2-diserverapps/6.png?raw=true)

* Melakukan npm install
```bash
  npm i
```
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/4-nvm-npm-pm2-diserverapps/7.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/4-nvm-npm-pm2-diserverapps/8.png?raw=true)

* Install pm2 secara global

```bash
  npm i -g pm2
```
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/4-nvm-npm-pm2-diserverapps/9.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/4-nvm-npm-pm2-diserverapps/10.png?raw=true)

* Ubah name dan script di dalam file ecosystem.config.js

```bash
  sudo nano ecosystem.config.js
```

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/4-nvm-npm-pm2-diserverapps/11.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/4-nvm-npm-pm2-diserverapps/12.png?raw=true)


* Jalankan aplikasinya dengan command
```bash
  pm2 start ecosystem.config.js
```

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/4-nvm-npm-pm2-diserverapps/13.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/4-nvm-npm-pm2-diserverapps/14.png?raw=true)

* Check apakah aplikasi sudah berjalan di web browser
dengan memasukkan ip server aplikasi disertai port nya

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/4-nvm-npm-pm2-diserverapps/15.png?raw=true)

___

### 6. Setting DNS di Cloudflare

* Pergi ke menu DNS. Lalu add record dan isi domain yang diinginkan lalu isi ipv4 address dengan ip web server

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/6-cloudflare/4.png?raw=true)

* Lalu simpan API key di webserver dengan cara pergi ke profile--API Tokens--view global api key

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/6-cloudflare/6.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/6-cloudflare/7.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/6-cloudflare/8.png?raw=true)

* Pergi ke webserver lalu buat directory .secret dan isi directory tersebut dengan file yang akan menampung API key dari cloudflare tadi

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/6-cloudflare/10.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/6-cloudflare/11.png?raw=true)

___

### 7. Start The App

* Check perubahan code dengan command dan restart nginx
```bash
sudo nginx -t
sudo systemctl restart nginx
```
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/7-jalanin-app/1.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/7-jalanin-app/2.png?raw=true)

* Lalu jalankan aplikasi di web browser dengan domain yang sudah di atur tadi

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/selasa/tugas/7-jalanin-app/3.png?raw=true)

___

# Rabu

## Database
<p> Database merupakan tempat dimana kita bisa memasukkan informasi yang telah di input oleh user dan memanagenya. Tanpa adanya database user tidak bisa membuat akun yang nantinya akan berdampak pada tidak bisa digunakannya aplikasi secara maksimal. Data yang di inputkan hanya sebatas tampilan saja jadi tidak tersimpan di server.</p>

Dalam database ada yang disebut sql dan nosql.
 
 <p>SQL : Sebuah bahasa standar query yang digunakan untuk mengatur, menampilkan dan membuat data didalm database</p>
 
 <p>NoSQL : Fungsinya sama seperti SQL namun lebih fleksibel karena bersifat tanpa relasi dan tidak membutuhkan query yang komplek dan lebih sering digunakan untuk sistem manajemen database untuk big data yang berubah-ubah</p>
 
 ## 1. Membuat Database mysql
 * Disini kita akan membuat server untuk database, pergi ke idcloudhost lalu pilih create new resource dan kustomisasi VM nya sesuai gambar

 ![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/1-create-database-mysql/1.png?raw=true)

 ![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/1-create-database-mysql/2.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/1-create-database-mysql/3.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/1-create-database-mysql/4.png?raw=true)

* Lalu masuk ke lokal dan akses VM database dengan SSH

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/1-create-database-mysql/5.png?raw=true)

* Install mysql server
```bash
sudo apt install mysql-server
```
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/1-create-database-mysql/7.png?raw=true)

* Check database apakah sudah aktif
```bash
sudo systemctl status mysql
```
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/1-create-database-mysql/8.png?raw=true)

* Lalu masuk ke dalam database denngan command
```bash
sudo mysql
```
* Buatlah user utama di database (root/lokal kita) dengan command
```bash
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by 'password kalian';
```
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/1-create-database-mysql/10.png?raw=true)

* Installasi secure mysql
```bash
sudo mysql_secure_installation
```
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/1-create-database-mysql/13.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/1-create-database-mysql/15.png?raw=true)

* Setelah selesai menginstall secure mysql lalu masuk database sebagai root

```bash
sudo mysql -u root -p
```
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/1-create-database-mysql/16.png?raw=true)

* Buat user baru di database dengan command
```bash
CREATE USER 'henry'@'%' IDENTIFIED BY 'password anda';

GRANT ALL PRIVILAGES ON *.* TO 'henry'@'%';

FLUSH PRIVILEGES;
```
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/1-create-database-mysql/19.png?raw=true)

* Masuk ke database sebagai user baru henry dengan command
```bash
sudo mysql -u henry -p
```
 ![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/1-create-database-mysql/20.png?raw=true)

* Buat database untuk aplikasi
```bash
CREATE DATABASE dumbflix;
```
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/1-create-database-mysql/22.png?raw=true)

* Lalu pergi ke file mysqld.cnf di directory /etc/mysql/mysql.conf.d/mysqld.cnf dan buka dengan text editor
* Ubah ip di bind-address dan mysqlx-bind-address menjadi 0.0.0.0

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/1-create-database-mysql/24.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/1-create-database-mysql/25.png?raw=true)

## 2. Clone Aplikasi Backend di Server Aplikasi

* Clone aplikasi ke server aplikasi dengan command
```bash
git clone <url aplikasi>
```
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/2-CloneApp-nvm-npm/1.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/2-CloneApp-nvm-npm/2.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/2-CloneApp-nvm-npm/3.png?raw=true)

* Buat ecosystem pm2 di directory aplikasi

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/2-CloneApp-nvm-npm/5.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/2-CloneApp-nvm-npm/6.png?raw=true)

* Install npm 
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/2-CloneApp-nvm-npm/7.png?raw=true)
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/2-CloneApp-nvm-npm/9.png?raw=true)

## 3. Sequelize dan Migrasi data

* install sequelize dengan command
```bash
npm i sequelize-cli -g
```
* Lalu check apakah sudah terinstall dengan command
```bash
sequelize
```
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/3-Sequelize-migration/1.png?raw=true)

* Menjalankan ketentuan deploy aplikasi backend dumbflix
yaitu copy .env.example ke .env , ubah config/config.json ke database kita , deploy dengan port 5000

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/3-Sequelize-migration/2.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/3-Sequelize-migration/3.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/3-Sequelize-migration/4.png?raw=true)

* Install npm lalu migrasi data backend ke database
menggunakan command

```bash
npm i
```
```bash
npx sequelize db:migrate
```
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/3-Sequelize-migration/6.png?raw=true)

* Pergi ke database lalu check apakah semua data sudah masuk di database
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/3-Sequelize-migration/9.png?raw=true)

## 4. Test aplikasi backend , masuk ke server aplikasi dan start aplikasi menggunakan pm2

```bash
pm2 start ecosystem.config.js
```
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/4-Test-backend/1.png?raw=true)

* Pergi ke web browser dan akses aplikasi backend dengan ip server aplikasi. 'Cannot GET' menandakan bahwa backend sudah bisa berjalan

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/4-Test-backend/3.png?raw=true)


## 5. Reverse proxy untuk backend

* Pergi ke webserver lalu buat file reverse proxy untuk backend di directory /etc/nginx/dumbflix

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/5-Reverseproxy-backend/1.png?raw=true)

* Isi file tersebut sesuai dengan gambar
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/5-Reverseproxy-backend/2.png?raw=true)

* Lalu check dan restart nginx
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/5-Reverseproxy-backend/3.png?raw=true)

## 6. Installasi Certbot

* Tetap di webserver lalu install certbot dengan command
```bash
sudo snap install core; sudo snap refresh core
```
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/6-Certbot/1.png?raw=true)

* Lalu masukkan command 
```bash
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/6-Certbot/2.png?raw=true)

* Lalu jalankan perintah, dan masukkan email kalian
```bash
sudo certbot
```
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/6-Certbot/3.png?raw=true)

* Pilih domain yang akan digunakan https
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/6-Certbot/5.png?raw=true)

* Installasi certbot sudah berhasil

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/6-Certbot/7.png?raw=true)

## 7. Ganti Base URL di api.js frontend
* Masuk ke directory aplikasi frontend di server aplikasi dan buka file api.js di src/config/
* Lalu ganti Base URL dengan domain backend tadi

[Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/7-GantiBaseURL-apijs-frontend/1.png?raw=true)

## 8. Jalankan Aplikasi

* Pergi ke server aplikasi lalu jalankan kedua aplikasi frontend dan backend dengan perintah 
```bash
pm2 start ecosystem.config.js
```
[Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/8-StartApp/1.png?raw=true)

[Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-1/rabu/tugas/8-StartApp/2.png?raw=true)




















