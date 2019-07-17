[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://paypal.me/matteoiervasi)
[![Gitter chat](https://badges.gitter.im/gitterHQ/gitter.png)](https://gitter.im/dell-xps-9570-ubuntu-respin/Lobby?utm_source=share-link&utm_medium=link&utm_campaign=share-link)

![DELL XPS 9570](https://github.com/jackhack96/dell-xps-9570-ubuntu-respin/raw/master/screenshot.png)

# DELL XPS 15 9570 Ubuntu 18.04 respin and post installation script (both 18.04 and 19.04)

### Table of Contents
1. [Post-install script](#post-install-script)
2. [Ready to use ISO](#ready-to-use-iso)
3. [Manual respin procedure](#manual-respin-procedure)
4. [Switching from one graphic card to the other](#how-to-switch-from-one-graphic-card-to-the-other)
5. [Troubleshooting](#troubleshooting)

Collection of scripts and tweaks to make Ubuntu 18.04 run smooth on Dell XPS 15 9570. The ISO has successfuly been used to install on other Dell laptops, such as the G5 15. 

I suggest everyone to use the post install method, the respun ISO is no longer neeeded for booting Ubuntu on 9570 as the stock one contains the needed fixes.

All informations, tips and tricks was gathered from:

- [tomwwright gist for DELL XPS 15 9560](https://gist.github.com/tomwwright/f88e2ddb344cf99f299935e1312da880)
- [Atheros wifi card fix](https://ubuntuforums.org/showthread.php?t=2323812&page=2)
- [Respin script and info](http://linuxiumcomau.blogspot.com/)
- Myself xD

Kudos and all the credits for things not related to my work go to developers and users on those pages!

### What works out-of-the-box

 - ✅ Atheros Wifi
 - ✅ Audio
 - ✅ Audio on HDMI
 - ✅ HDMI ( even on lid closed )
 - ✅ Nvidia/Intel graphic cards switch
 - ✅ Keyboard backlight
 - ✅ Display brightness
 - ✅ Sleep/wake on Intel

### What does't work properly
 - ➖ Sleep/wake on nVidia

### What doesn't work at the moment

 - ❌ Goodix Fingerprint sensor

## Post-install script
If you already have a standard Ubuntu install, you can try applying basic tweaks with the `xps-tweaks.sh` script.
You can run it directly without cloning the repository with the following command (requires `curl`):
```shell
bash -c "$(curl -fsSL https://raw.githubusercontent.com/JackHack96/dell-xps-9570-ubuntu-respin/master/xps-tweaks.sh)"
```

## Ready to use ISO
You can download an already respun ISO [here](https://drive.google.com/open?id=1FzOQTGXLFp_F6MxKerwicirCF2juylcO).

## Manual respin procedure

1. [Clone the repo and install necessary tools](#step-1-cloning-the-repo-and-installing-tools)
2. [Download your Ubuntu 18.04 ISO](#step-2-download-your-ubuntu-1804-iso)
3. [Respin the ISO (it many take a about 30 minutes or even longer)](#step-3-build-your-respun-iso)
4. [Install OS and run post-install commands](#step-4-install-and-update)

### Step 1: Cloning the Repo and Installing Tools

To respin an existing Ubuntu ISO, you will need to use a Linux machine with some packages like `squashfs-tools` and `xorriso` installed (e.g. `sudo apt install -y squashfs-tools xorriso`) and a working internet connection. Script require at least 10GB of free storage space.

The first step is to clone this repo: 
```
git clone https://github.com/jackhack96/dell-xps-9570-ubuntu-respin.git
cd dell-xps-9570-ubuntu-respin/
```
#### Debian-based systems:

Install all the required packages:
```
sudo apt install -y git wget genisoimage bc squashfs-tools xorriso
```
#### Arch-Based Systems:

Install all the required packages:
``` 
sudo pacman -S git wget cdrkit bc libisoburn squashfs-tools dosfstools
```

### Step 2: Download your Ubuntu 18.04 ISO

Download Ubuntu 18.04 ISO and copy it in this repository cloned folder.

### Step 3: Build Your Respun ISO

Run `./build.sh` script like this:
```shell
./build.sh -i <iso filename>
``` 
There are also two flags you can set for enabling other options:
- The `v` flag will autoinstall video codecs if set to  `true`
- The `s` flag will disable SPECTRE/Meltdown patches for additional performance if set to `false`

Run `./build.sh -h` for help.

### Step 4: Install and Update

#### Boot ISO from USB device

I suggest [Etcher](https://etcher.io/) to write ISO on usb flash drives.
It's fast, reliable and multi-platform.

Boot system using one time boot menu.
Disable Secure boot in bios to boot from the ISO.

### Post-install notes

If you want touchpad gestures, check https://github.com/bulletmark/libinput-gestures.

## How to switch from one graphic card to the other

Intel:
```
sudo prime-select intel
```
Nvidia:
```
sudo prime-select nvidia
```

**Note: A full reboot could be required when switching graphic cards.**

## Troubleshooting

Check the [wiki page](https://github.com/JackHack96/dell-xps-9570-ubuntu-respin/wiki/Troubleshooting) about it.
