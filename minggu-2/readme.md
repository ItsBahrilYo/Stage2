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
IMAGE

### 2.

* Jalankan dockerfile untuk membuat image dari aplikasi kita
```bash
docker build -t yubisayu/housy-be:1.0 .
```
IMAGE


### 3.
* Chekc images apakah sudah terbuat
```bash
IMAGE
```
### 4.
* Push images yang sudah dibuat tadi ke repository di akun docker hub

```bash
docker push yubisayu/housy-fe:stable
```
IMAGE DI TERMINAL DAN
IMAGE REPO DI DOCKER HUB

### 5.
*Buat docker container
```bash
docker container create --name database -v /home/mentor/wayshub:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=(password) -e MYSQL_DATABASE=wayshub mysql:latest
```

IMAGE

### 6.
*Jalan kan docker container

```bash
docker run -d --name housy-fe -p 3306:3306 yubisayu/housy-fe:stable
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










