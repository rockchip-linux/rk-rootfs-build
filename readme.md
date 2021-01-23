## Introduction

A set of shell scripts that will build GNU/Linux distribution rootfs image
for rockchip platform.

## Available Distro

* Debian 10 (Buster-X11 and Wayland)~~

```
sudo apt-get install adduser debian-archive-keyring fdisk gcc-8-base gpgv \
    libacl1 libapt-pkg5.0 libattr1 libaudit-common libaudit1 libblkid1 libbz2-1.0 \
    libc6 libcap-ng0 libcom-err2 libdb5.3 libdebconfclient0 libext2fs2 libfdisk1 \
    libffi6 libgcc1 libgcrypt20 libgmp10 libgnutls30 libgpg-error0 libhogweed4 \
    libidn2-0 liblz4-1 liblzma5 libmount1 libncursesw6 libnettle6 libp11-kit0 \
    libpam0g libpcre3 libseccomp2 libselinux1 libsemanage-common libsemanage1 \
    libsepol1 libsmartcols1 libss2 libstdc++6 libsystemd0 libtasn1-6 libtinfo6 \
    libudev1 libunistring2 libuuid1 libzstd1 zlib1g
sudo apt-get install dirmngr gnupg-l10n gnupg-utils gpg gpg-agent \
    gpg-wks-client gpg-wks-server gpgconf gpgsm libassuan0 libksba8 libldap-2.4-2 \
    libldap-common libnpth0 libreadline7 libsasl2-2 libsasl2-modules-db libsqlite3-0 \
    libssl1.1 lsb-base openssl pinentry-curses readline-common
sudo apt-get install binfmt-support qemu-user-static python-dbus python-debian \
    python-yaml python-apt
sudo dpkg -i ubuntu-build-service/packages/*
sudo apt-get install -f
```

## Usage for 32bit Debian 10 (Buster-32)

Building a base debian system by ubuntu-build-service from linaro.

```
	RELEASE=buster TARGET=desktop ARCH=armhf ./mk-base-debian.sh
```

Building the rk-debian rootfs:

```
	RELEASE=buster ARCH=armhf ./mk-rootfs.sh
```

Building the rk-debain rootfs with debug:

```
	VERSION=debug ARCH=armhf ./mk-rootfs-buster.sh
```

Creating the ext4 image(linaro-rootfs.img):

```
	./mk-image.sh
```

---

## Usage for 64bit Debian 10 (Buster-64)

Building a base debian system by ubuntu-build-service from linaro.

```
	RELEASE=buster TARGET=desktop ARCH=arm64 ./mk-base-debian.sh
```

Building the rk-debian rootfs:

```
	RELEASE=buster ARCH=arm64 ./mk-rootfs.sh
```

Building the rk-debain rootfs with debug:

```
	VERSION=debug ARCH=arm64 ./mk-rootfs-buster.sh
```

Creating the ext4 image(linaro-rootfs.img):

```
	./mk-image.sh
```
---

## Cross Compile for ARM Debian

[Docker + Multiarch](http://opensource.rock-chips.com/wiki_Cross_Compile#Docker)

## Package Code Base

Please apply [those patches](https://github.com/rockchip-linux/rk-rootfs-build/tree/master/packages-patches) to release code base before rebuilding!

## FAQ

- noexec or nodev issue
noexec or nodev issue /usr/share/debootstrap/functions: line 1450:
../rootfs/ubuntu-build-service/stretch-desktop-arm64/chroot/test-dev-null:
Permission denied E: Cannot install into target
...
mounted with noexec or nodev

Solution: mount -o remount,exec,dev xxx (xxx is the mount place), then rebuild it.
