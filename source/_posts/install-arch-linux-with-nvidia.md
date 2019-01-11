---
title: How-To | Install Arch Linux with Nvidia GeForce 1080Ti
date: 2017-11-08 09:43:38
tags:
  - Installation
  - Linux
categories:
  - How-To
---
## Download Arch and Verify ISO
https://www.archlinux.org/download/
pg --keyserver-options auto-key-retrieve --verify archlinux-<version>-x86_64.iso.sig

## Create Installation Medium
dd bs=4M if=/path/to/archlinux.iso of=/dev/sdx status=progress && sync

## Arch Installation Guide
https://wiki.archlinux.org/index.php/installation_guide#Install_the_base_packages

### Partition Scheme
```config
/boot	/dev/sdx1	EFI System Partition (EF00)	    More than 512 MiB
/	    /dev/sdx2	Linux	                        70 GB
/home	/dev/sdx4	Linux	                        Rest
```

Example:
```bash
Partition number (3-128, default 3):  3 
First sector (34-15728606, default = 4605952) or {+-}size{KMGTP}: 
Last sector (4605952-15728606, default = 15728606) or {+-}size{KMGTP}: +4G
Current type is 'Linux filesystem'
Hex code or GUID (L to show codes, Enter = 8300): 8300
Changed type of partition to 'Linux filesystem
```

+ Make Swap-File
```bash
fallocate -l 8GB /swapfile
chmod 600 /swapfile
mkswap /swapfile
swapon /swapfile

~ vim /etc/fstab
    /swapfile none swap defaults 0 0
```

+ Installation of KDE Plasma (NVIDIA)
https://sadanand-singh.github.io/posts/completesetuparchplasma/
```bash
$ pacman -S xorg-server nvidia nvidia-libgl nvidia-settings mesa
$ pacman -S ttf-hack ttf-anonymous-pro
$ pacman -S ttf-dejavu ttf-freefont ttf-liberation
$ pacman -S plasma-meta dolphin kdialog kfind
$ pacman -S konsole gwenview okular spectacle kio-extras
$ pacman -S kompare dolphin-plugins kwallet kwalletmanager
$ pacman -S ark yakuake flite
```

+ SDDM
```bash
$ vim /etc/sddm.conf

....
[Theme]
# Current theme name
Current=breeze

# Cursor theme used in the greeter
CursorTheme=breeze_cursors
...

$ systemctl enable sddm
$ reboot
```
