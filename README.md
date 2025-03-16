# Install Ubuntu + Xfce di MacOS

Kita bisa menggunakan multipass untuk membuat sebuah virtual machine Ubuntu dan menginstall Xfce. Kita dapat mengakses desktop Xfce ini melalui Remote Desktop Protocol.

## Mengapa?

1. VM dapat digunakan untuk development, testing, sandboxing.
2. VM dapat digunakan untuk keperluan anonymous / pseudonym.
3. VM dapat di-install apa pun tanpa mengganggu Host (MacOS).
4. Ketika sudah tidak dibutuhkan bisa dihapus dengan mudah, tanpa jejak.

## Prasyarat

1. Multipass di MacOS. Cara instalasi ada di: https://canonical.com/multipass/docs/install-multipass

2. Microsoft Remote Desktop. Bisa diinstall dari Mac App Store. Sekarang namanya Windows App for Mac.

## Buat VM Ubuntu di Multipass

Saya akan membuat VM Ubuntu di MacOS dengan nama xfce, 2 CPU, 2GB RAM, dan 8GB Storage. Berikut perintahnya:

```
multipass launch --name xfce -c 2 -m 2g -d 8g
```

Tunggu sampai selesai prosesnya.

## Buat user baru di VM

Masuk ke VM tsb

```
multipass shell xfce
```

Setelah masuk, buat user baru. Sebagai contoh, saya membuat user dengan nama "dewo". Silakan sesuaikan dengan kebutuhan.

```
sudo adduser dewo
sudo adduser dewo root sudo
```

## Install & setup xfce dan xrdp di VM

Install xfce di VM

```
sudo apt update
sudo apt install xfce4 xfce4-goodies -y
```

Kemudian install xrdp di VM

```
sudo apt install xrdp -y
```

Cek apakah sudah berhasil berjalan?

```
sudo systemctl status xrdp
```

Jika belum berjalan, maka jalankan perintah berikut:

```
sudo systemctl start xrdp
```

## Konfigurasikan sesi xfce untuk user

Di atas saya sudah buat user "dewo". Sekarang kita setup sesi default desktop untuk user tsb.

```
su dewo

cd ~

echo "xfce4-session" | tee .xsession

sudo systemctl restart xrdp
```

Secara default audio akan dimainkan di audio-dummy. Tidak akan bunyi.

Supaya audio bisa disalurkan ke Host (via pipewire), maka pastikan modul-modul pipewire sudah terinstall (secara default sudah terinstall).

```
sudo apt list pipewire-*
```

install juga pipewire-audio dan pipewire-pulse.

```
sudo apt install pipewire-audio pipewire-pulse
sudo pulseaudio -k
```

Kill pulseaudio dengan -k, nanti akan jalan lagi. Tapi jika belum berhasil, maka reboot VM dulu.

Catat IP dari VM untuk dapat diakses dari MacOS via Remote Desktop.

```
hostname -I
```

## Akses VM dari MacOS menggunakan Remote Desktop

Buka aplikasi Remote Desktop. Tambahkan PC. Masukkan IP-nya. Kemudian klik "Connect".

Masukkan username & password.

Coba install browser & mainkan video youtube dari channel @orang_it

Semoga berhasil.


## Xenara Cafe and Coworking Space

Ruko Citra Grand, Blok London C-08, Semarang, Indonesia
