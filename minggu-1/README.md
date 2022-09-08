# Hi There! Welcome
Kali ini saya akan menjelaskan tentang cloud computing menggunakan idcloudhost, managed database dan setup backend sederhana 

## Cloud Computing dengan IDCH
<p>Cloud computing merupakan teknologi memvirtualisasi resource berupa server yang dimana kita bisa mendapatkan aksesnya dan mengkostumisasi system requirementnya (core, memory, disk) melalui jaringan.

IDCH (idcloudhost) merupakan suatu web hosting provider yang ada di Indonesia yang menawarkan layanan seperti pendaftaran domain, cloud hosting, server (VPS & Dedicated Server) dan masih banyak lagi</p>
___
 ### 1. Membuat VM di idcloudhost
  
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

