FROM ubuntu:focal
MAINTAINER Giulio Benetti <giulio.benetti@benettiengineering.com>

LABEL maintainer="Giulio Benetti <giulio.benetti@benettiengineering.com>" \
description="Container with everything needed to build Rockchip Debian"

ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Europe/Rome

RUN set -e; \
  apt-get update; \
  apt-get install -y apt-utils; \
  apt-get upgrade -y; \
  apt-get install -y locales;

RUN set -e; \
  rm -rf /var/lib/apt/lists/*; \
  localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8

# Setup tzdata first as to avoid a dialog requesting tzdata setup.
RUN set -e; \
  apt-get update; \
  apt-get install -y tzdata; \
  ln -snf /usr/share/zoneinfo/$TZ /etc/localtime; \
  echo $TZ > /etc/timezone;

# Install basic dependencies
RUN set -e; \
  apt-get upgrade -y; \
  apt-get install -y \
  bc \
  bash-completion \
  bison \
  bzip2 \
  cmake \
  cpio \
  dialog \
  expect \
  file \
  flex \
  g++ \
  gcc \
  git \
  lib32z1 \
  make \
  mc \
  nano \
  ncurses-dev \
  patch \
  rsync \
  sudo \
  tar \
  unzip \
  wget

# Install rk-rootfs-build specific depdendencies
RUN set -e; \
  apt-get install -y \
  debootstrap schroot \
  adduser debian-archive-keyring fdisk gcc-8-base gpgv libacl1 libapt-pkg6.0 \
  libattr1 libaudit-common libaudit1 libblkid1 libbz2-1.0 libc6 libcap-ng0 \
  libcom-err2 libdb5.3 libdebconfclient0 libext2fs2 libfdisk1 libffi7 libgcc1 \
  libgcrypt20 libgmp10 libgnutls30 libgpg-error0 libhoweed5 libidn2-0 \
  liblz4-1 liblzma5 libmount1 libncursesw6 libnettle7 libp11-kit0 libpam0g \
  libpcre3 libseccomp2 libselinux1 libsemanage-common libsemanage1 libsepol1 \
  libsmartcols1 libss2 libstdc++6 libsystemd0 libtasn1-6 libtinfo6 libudev1 \
  libunistring2 libuuid1 libzstd1 zlib1g dirmngr gnupg-l10n gnupg-utils gpg \
  gpg-agent gpg-wks-client gpg-wks-server gpgconf gpgsm libassuan0 libksba8 \
  libldap-2.4-2 libldap-common libnpth0 libreadline8 libsasl2-2 \
  libsasl2-modules-db libsqlite3-0 libssl1.1 lsb-base openssl pinentry-curses \
  readline-common binfmt-support qemu-user-static python-dbus python-debian \
  python-yaml python-apt dosfstools parted python python-argparse python-dbus \
  python-debian python-parted-doc python-yaml u-boot-tools python-apt

# Python3
RUN set -e; \
  apt-get install -y \
  python-dev \
  python3-dev \
  python3-pip;

RUN set -e; \
  pip3 install \
  nose2==0.9.2 \
  pexpect==4.8.0;

RUN useradd -ms /bin/bash rkdeb-user
RUN usermod -aG sudo rkdeb-user
RUN echo "alias ls='ls --color=auto'" >> /home/rkdeb-user/.bashrc
RUN echo "PS1='\u@\H [\w]$ '" >> /home/rkdeb-user/.bashrc
RUN chown -R rkdeb-user:rkdeb-user /home/rkdeb-user

USER rkdeb-user
WORKDIR /home/rkdeb-user
ENV HOME /home/rkdeb-user

CMD ["/bin/bash"]
