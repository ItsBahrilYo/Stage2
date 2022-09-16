# DOCKER
 ## Docker 
  Merupakan suatu open platform yang melayani sistem komputasi virtual untuk memproduksi, mengirim, testing, deploy dan menjalankan software dalam bentuk package yang disebut container

  ## Container
  Suatu lingkungan package yang terisolasi untuk membungkus dan mejalankan aplikasi. Di dalamnya mengandung apapun yang dibutukan untuk menjalankan aplikasi seperti library, dependencies dll  

  ## Images
  Merupakan sebuah template image read-only yang di dalamnya berisi instruksi untuk membuat docker container. Kita bisa membuat image kita sendiri dan juga bisa menggunakan image lain yang sudah terpublish di docker registry. Untuk membuat image sendiri kita perlu membuat Dockerfile yang berisikan syntax untuk mendefinisikan langkah-langkah yang dibutuhkan untuk membuat image dan menjalankannya.

## Mengapa menggunakan Docker? 

* Karena docker memudahkah siklus pengembangan aplikasi dengan menmberikan developer lingkungan terstadarisasi berupa container yang melayani aplikasi kita dengan beberapa service.  
* Containers sendiri sangat bagus untuk proses CICD, karena para developer dapat menuliskan kode mereka secara lokal dan bisa saling share code mereka menggunakan docker container
* Developer dapat menge-push aplikasi mereka ke staging environtment, mengeksekusi secara automasi dan melakukan manual test
* Ketika menemukan bugs developer dapat memperbaikinya di development environment lalu redeploy aplikasi ke test environment untuk test dan memvalidasinya
* Docker lebih responsive dalam deployment  dan scalling karena pembagian beban kerja yang sangat efisien antar resource dan sangat portable bisa di gunakan di local laptop, physical/virtual machine di data center, di cloud provider ataupun di lingkungan yang bercampur.

# Arsitektur Docker
![Markdown Logo](https://docs.docker.com/engine/images/architecture.svg)

## Docker Daemon
 Docker daemon bertugas untuk menerima request berupa docker API dan memanage objek docker seperti images, container, network dan volumes. Dan daemon dapat berkomunikasi dengan daemon yang lain untuk memanage layanan docker.
 
## Docker Client
Merupakan sebuah cara yang digunakan docker user untuk  berinteraksi dengan sistem docker. Dengan kita menjadi docker user kita bisa mengirimkan perintah kepada Docker Daemon (dockerd) dan akan memproses apa yang kita perintahkan. Perintah docker menggunankan docker API. Docker Client dapat berkomunikasi lebih dari satu daemon.

## Docker Registry
Sebuah tempat atau storage untuk docker image. Image yang sama dapat memiliki beberapa versi dan teridentifikasi dengan tag yang di buat. Docker registry terogarnisir ke dalam docker repository yang dimana repository tersebut menyimpan semua versi dari images tertentu.

# Fitur penting dalam docker

## Docker Build
Build adalah kunci utama perkembangan software dimana kita dapat membungkus code-code kita dan mengirimnya kemana saja. Metode yang paling umum digunakan untuk build adalah perintah docker build dilakukan di docker CLI lalu CLI mengirimkan request tersebut ke Docker Engine yang akan mengeksekusi build kita.

### Dockerfile 
Apa yang kita build sebenarnya adalah sebuah dockerfile dimana dockerfile ini merupakan file yang berisikan text instruksi. Jadi Docker akan build images dengan membaca instruksi yang ada di dalam dockerfile. Ada beberapa perintah yang sering di gunakan seperti:
    
 * FROM : Mendefinisikan images kita
 * RUN  :Mengeksekusi perintah 
 * WORKDIR : Mengatur working directory untuk  perintah (RUN, CMD, ENTRYPOINT, COPY, ADD dan lain-lain)
 * COPY : Copy file/directory dari <src> dan menambahkannya ke file sistem dari container
* CMD : Mejalankan perintah default untuk image yang kita build		

## Docker Compose
Merupakan sebuah tool untuk mendefinisikan dan menjalankan aplikasi secara multi-container. Di compose kita menggunakan file berekstensi YAML untuk megkonfigurasi service aplikasi kita. Dengan satu command kita bisa membuat dan memulai semua services dari konfigurasi yang kita buat. Compose bekerja disemua environment (staging, development, testing dll).

___



## Frontend App in Docker
### 1.
* Buat file dengan nama dockerfile lalu masukkan konfigurasi dibawah ini ke dalam file tersebut
```bash
FROM node:10
WORKDIR /usr/app
COPY . .
RUN npm install
EXPOSE 3000
CMD [ "npm", "start" ]
```
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-2/docker/dockerfilebe.png?raw=true)

### 2.

* Jalankan dockerfile untuk membuat image dari aplikasi kita
```bash
docker build -t yubisayu/housy-be:1.0 .
```
IMAGE


### 3.
* Chekc images apakah sudah terbuat

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-2/docker/checkimages.png?raw=true)

### 4.
* Push images yang sudah dibuat tadi ke repository di akun docker hub

```bash
docker push yubisayu/housy-fe:stable
```
![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-2/docker/pushimagefe.png?raw=true)

![Markdown Logo](https://github.com/ItsBahrilYo/Stage2/blob/master/minggu-2/docker/hosydidockerhub.jpeg?raw=true)


### 5.
*Buat docker container
```bash
docker container create --name housy-frontend -p 3000:3000 yubisayu/housy-fe:1.0
```

IMAGE

### 6.
*Jalan kan docker container

```bash
docker run -d --name housy-fe -p 3000:3000 yubisayu/housy-fe:stable
```

### 7.

* Buat file docker compose berektensi .yaml lalu masukkan konfigurasi dibawah ini ke dalam file tersebut
```bash
version: '3.8'
services:
 frontend:
   build: .
   container_name: fe
   image: yubisayu/housy-fe:stable
   stdin_open: true
   ports:
    - 3030:3000
```
IMAGE
### 8.
* Jalankan docker compose
```bash
docker compose up -d
```


## Mengintegrasikan Aplikasi Frontend dan Backend

### 1.
* Masuk ke dalam directory frontend lalu ke dalam file api.js dan ubah BaseURL menjadi domain dari backend

IMAGE
### 2.
* Lalu check aplikasi pada web browser

##  Backend App in Docker

### 1.
* Clone aplikasi yang sudah tersedia dari github
```bash
git clone https://github.com/dumbwaysdev/housy-backend.git
```

IMAGE

### 2.
* Ikuti perintah yang ada di dalam file readme.md
IMAGE

IMAGE API.JS DAN REVERSEP

### 3. 
* Lalu edit file config.json di dalam directory config/config.json

IMAGE 

### 4.
* Buat Dockerfile dengan konfigurasi seperti dibawah
```bash
FROM node:10
WORKDIR /usr/app
COPY . .
RUN npm install
RUN npm install sequelize-cli -g
RUN npx sequelize db:migrate
EXPOSE 5000
CMD [ "npm", "start" ]
```
IMAGE
 
### 5.
* Buat file docker compose dengan ekstensi yaml lalu isi file dengan konfigurasi sepeerti di bawah

```bash
version: '3.8'
services:
 backend:
   build: .
   container_name: housy-backend
   image: yubisayu/housy-be:1.0
   stdin_open: true
   ports:
    - 5000:5000
```
IMAGE
### 6. 
* Build docker compose dengan perintah seperti di bawah
```bash
docker compose up -d
```
IMAGE

### 7.
* Check aplikasi apakah sudah berjalan
IMAGES

### 8. 
* Membuat database menggunakan mysql. Pull image mysql yang ada di docker registry menggunakan perintah di bawah
```bash
docker pull mysql
```
IMAGE
### 9.
* Lalu buat container yang didalamnya sudah terinstall database mysql
```bash
docker container create --name database -v /home/kelompok4/housy:/var/lib/mysql -e  MYSQL_ROOT_PASSWORD=(password anda) -e MYSQL_DATABASE=housy mysql:latest    
```
IMAGE

### 10. 
* Check apakah container database sudah ada
IMAGE

### 11.
* Push image ke dockerhub.com
IMAGE

### 12. Setting reverse proxy dan menggunakan certbot

* Masuk ke cloudflare dan tambahkan dns 
(frontend)

IMAGE

(backend)

IMAGE


* Lakukan update lalu install nginx
```bash
sudo apt update
sudo apt install nginx
```
IMAGE

### Reverse proxy
* Membuat reverse proxy dengan buat directory di dalam /etc/nginx yang nantinya akan diisi file reverse proxy

IMAGE

* Ubah ownership dari dorectory tersebut untuk user 
 IMAGE

* Buar file reverse proxy dengan txt editor nano dan isikan file didalam dengan perintah seperti dibawah

```bash
server {
    server_name <domain anda>;

    location / {
        proxy_pass http:// <ip server aplikasi>:<port>;
    }
}
```
IMAGE FE
IMAGE BE

* Lalu pergi ke directory /etc/nginx/ dan buka file nginx.conf lalu masukkan directory dari reverse proxy tadi

IMAGE

* Check perubahan dan restart nginx
```bash
sudo nginx -t
sudo systemctl restart nginx
```
### Certbot
* Masuk certbot dengan cara
```bash
sudo certbot
```
* Lalu ikuti perintah seperti pada gambar



IMAGE



IMAGE



IMAGE


* Check apakah certbot sudah berjalan dengan masuk ke file reverse proxy backend dan lihat apakah ada penambahan code dari certbot

IMAGE










