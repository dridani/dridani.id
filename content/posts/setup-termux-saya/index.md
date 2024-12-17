---
title: "Setup Termux Saya"
Slug: "setup-termux-saya"
date: 2024-10-10
categories:
  - Termux
tags:
  - Termux
  - Setup
summary: "Hal yang saya lakukan pertama kali saat setelah menginstal termux"
DescriptionSEO: "Cara setup termux untuk pemula"
description: ""
comments: false
draft: false
---

## Persiapan

Hal yang pertama kali saya lakukan setelah aplikasi termux terinstal di hp adalah melakukan persiapan dengan melakukan beberapa konfigurasi sederhana, sebagai berikut.

- Mengubah Lokasi Mirror

```shell
termux-change-repo
```

> Di sini saya memilih **Single Mirror** - **DomaiNesia**

- Mengizinkan Akses Penyimpanan

```shell
termux-setup-storage
```

- Update dan Upgrade Package

```shell
pkg update && pkg upgrade -y
```

---

## Menghubungkan Termux ke Github

Karena sebagian besar penggunaan termux saya digunakan untuk mengelola repositori github, maka di sini saya perlu menghubungkan termux ke akun github saya.

- Install `Git`

```shell
pkg install git -y
```

- Membuat Folder SSH

```shell
mkdir .ssh && cd .ssh
```

- Membuat **Public Key** dan **Private Key**

```shell
ssh-keygen -t ed25519 -C "emailkamu@gmail.com"
```

>  Disini akan muncul permintaan untuk mengisikan sesuatu, ==tidak perlu mengisinya== lewati saja semua dengan menekan `Enter`

- Salin Isi Public Key

```shell
cat id_ed25519.pub
```

- Tempel Isi Public Key

Tempelkan isi public key yang telah di salin ke akun GitHub, atau klik link berikut ini https://github.com/settings/keys

- Jalankan SSH Agent

```shell
eval "$(ssh-agent -s)"
```

- Menambahkan Identitas

```shell
ssh-add id_ed25519
```

- Tes konek ke akun Github

```shell
ssh -T git@github.com
```

> Di sini akan muncul permintaan, maka izinkan saja dengan mengetikan `yes` lalu tekan `Enter`

---

## Mengganti Shell Bawaan Menjadi ZSH

Tidak seperti shell bawaan termux yaitu Bash, menggunakan ZSH memberikan kita opsi untuk mengkustomisasi tampilan shell yang lebih atraktif dan eye catching.

Karena itu saya memilih menggunakan ZSH sebagai shell default di termux saya dan memasangkan beberapa plugin pendukung.

- Instal ZSH

```shell
pkg install zsh
```

- Jadikan ZSH Sebagai Shell Bawaan

```shell
chsh -s zsh
```

- Restart Termux

Keluar dari aplikasi termux atau tekan `CTRL + D` lalu buka kembali aplikasi termux

---

## Kustomisasi ZSH

Karena saya sudah menjadikan ZSH sebagai shell default, maka belum afdol rasanya jika belum menambahkan beberapa kustomisasi dan plugin pendukung.

Disini saya juga akan mengganti tulisan welcome termux menjadi Neofetch.

- Instal Neofetch

```shell
pkg install neofetch -y
```

- Mengganti tulisan Welcome Termux

```shell
nano ../usr/etc/zshrc
```

Setelah masuk, maka tambahkan tulisan `neofetch` di baris paling bawah.

> Oiya, jika kamu pengguna shell `bash`, ganti tujuannya ke `bashrc` seperti ini

```shell
nano ../usr/etc/bash.bashrc
```

Lalu simpan dengan menekan `CTRL + X` lalu `y` dan `Enter`

- Menghapus Tulisan Welcome Termux

Karena tulisan welcome termux sudah tidak dibutuhkan, maka hapus saja dengan mengetik

```shell
rm ../usr/etc/motd
```

- Instal oh-my-zsh

```shell
sh -c "$(wget -O- https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

- Instal Plugin Auto Suggestions

```shell
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

- Instal Plugin Syntax Highlighting

```shell
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

- Mengaktifkan Plugin

```shell
nano ~/.zshrc
```

Cari tulisan

```shell
plugins=(git)
```

Lalu ganti jadi seperti ini

```shell
plugins=(
git
zsh-autosuggestions
zsh-syntax-highlighting
)
```

- Terakhir restart aplikasi termux dan FINISH.

Jika ingin, kamu juga bisa menggunakan setup ini atau menyesuaikannya lagi sesuai kebutuhanmu.