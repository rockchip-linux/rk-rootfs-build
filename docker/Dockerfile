FROM ubuntu:focal
MAINTAINER Adam Duskett <aduskett@gmail.com>

LABEL maintainer="Adam Duskett <aduskett@gmail.com>" \
description="Container with everything needed to run Buildroot"

ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=US/Pacific

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

# Install dependencies
RUN set -e; \
  apt-get upgrade -y; \
  apt-get install -y \
  bc \
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
  mercurial \
  nano \
  ncurses-dev \
  patch \
  rsync \
  subversion \
  sudo \
  tar \
  unzip \
  wget

# 32-bit support.
RUN set -e; \
  apt-get install -y \
  gcc-multilib \
  g++-multilib \
  libc6-i386

# Python2 is needed for utils/scanpy
# Python3 is needed for support/testing/run-tests
RUN set -e; \
  apt-get install -y \
  python-dev \
  python3-dev \
  python-pip \
  python3-pip;

RUN set -e; \
  pip2 install \
  nose2==0.9.2 \
  pexpect==4.8.0 \
  spdx_lookup==0.3.2; \
  pip3 install \
  nose2==0.9.2 \
  pexpect==4.8.0;


RUN useradd -ms /bin/bash br-user
RUN echo "alias ls='ls --color=auto'" >> /home/br-user/.bashrc
RUN echo "PS1='\u@\H [\w]$ '" >> /home/br-user/.bashrc
RUN chown -R br-user:br-user /home/br-user

COPY brmake /usr/bin

USER br-user
WORKDIR /home/br-user
ENV HOME /home/br-user

CMD ["/bin/bash"]
