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

Bagi saya, termux adalah salah satu aplikasi yang sangat sering saya gunakan. Mulai dari mengatur performa hp, mengendalikan server, bahkan blog ini pun terkadang saya kelola dari termux kalo lagi malas buka laptop.

Nah! Agar aplikasi termux bisa berjalan dan dapat menunjang kebutuhan saya, maka ada beberapa hal yang perlu saya lakukan.

Jika ingin, Anda juga bisa menggunakan setup ini atau menyesuaikannya lagi dengan kebutuhan Anda.

## Persiapan

Setelah menginstal termux biasanya saya akan melakukan beberapa persiapan dasar terlebih dulu sebelum lanjut ke langkah yang sebenarnya.

- Mengubah Lokasi Mirror

```shell
termux-change-repo
```

> Di sini saya memilih **Single Mirror** - **DomaiNesia**

- Izinkan Akses penyimpanan

```shell
termux-setup-storage
```

- Perbarui Package

```shell
pkg update && pkg upgrade -y
```

---

## Menghubungkan Termux ke Github

- Instal Git

```shell
pkg install git
```

- Membuat Folder SSH

```shell
mkdir .ssh && cd .ssh
```

- Membuat **Public Key** dan **Private Key**

```shell
ssh-keygen -t ed25519 -C "emailkamu@gmail.com"
```

> Nanti akan muncul permintaan untuk mengisikan sesuatu, disini skip saja semua dengan menekan `Enter`

- Salin Isi Public Key

```shell
cat id_ed25519.pub
```

- Tempel Isi Public Key

Tempel isi public key yang tadi telah di salin ke GitHub atau klik link berikut https://github.com/settings/keys

- Jalankan SSH Agent

```shell
eval "$(ssh-agent -s)"
```

- Menambahkan Identitas

```shell
ssh-add id_ed25519
```

- Tes Konek Ke Github

```shell
ssh -T git@github.com
```

> Di sini akan muncul pilihan **yes/no**, maka izinkan saja dengan mengetikan `yes` lalu tekan `Enter`

---

## Mengganti Shell Bawaan Jadi ZSH

- Instal ZSH

```shell
pkg install zsh
```

- Jadikan ZSH Sebagai Shell Bawaan

```shell
chsh -s zsh
```

- Restart Termux

Tekan `CTRL + D` dan buka kembali aplikasi termux

---

## Kustomisasi ZSH

Saya ingin mengganti tulisan Welcome Termux menjadi neofetch.

- Instal Neofetch

```shell
pkg install neofetch
```

- Menghapus Tulisan Welcome Termux

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

- Edit File zshrc

```shell
nano ~/.zshrc
```

- Cari tulisan

```shell
plugins=(git)
```

- Ganti jadi seperti ini

```shell
plugins=(
git
zsh-autosuggestions
zsh-syntax-highlighting
)
```

- Keluar dan Save 

	- Tekan tombol `CTRL + X` 
	- lalu `y` 
	- dan `Enter`
- Masuk lagi ke aplikasi termux

Maka dengan ini selesai