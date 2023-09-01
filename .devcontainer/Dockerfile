FROM ubuntu:latest

# 元数据
LABEL org.opencontainers.image.ref.name=ubuntu
LABEL org.opencontainers.image.version=22.04
LABEL maintainer="mengplus" email="chengmeng_2@outlook.com"
# build参数
ARG user=uboot

ENV TZ=Asia/Shanghai

RUN sed -i "s@http://.*archive.ubuntu.com@http://repo.huaweicloud.com@g" /etc/apt/sources.list \
	  && sed -i "s@http://.*security.ubuntu.com@http://repo.huaweicloud.com@g" /etc/apt/sources.list \
      && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone \
      && apt-get update \
      && apt-get install -y gcc gcc-aarch64-linux-gnu gcc-arm-linux-gnueabi \
       bc bison build-essential coccinelle \
       device-tree-compiler dfu-util efitools flex gdisk graphviz imagemagick \
       liblz4-tool libgnutls28-dev libguestfs-tools libncurses-dev \
       libpython3-dev libsdl2-dev libssl-dev lz4 lzma lzma-alone openssl \
       pkg-config python3 python3-asteval python3-coverage python3-filelock \
       python3-pkg-resources python3-pycryptodome python3-pyelftools \
       python3-pytest python3-pytest-xdist python3-sphinxcontrib.apidoc \
       python3-sphinx-rtd-theme python3-subunit python3-testtools \
       python3-virtualenv swig uuid-dev \
       make \
      && apt-get install -y sudo vim tree \
      && apt-get autoremove && apt-get autoclean \
      && rm -rf /var/lib/apt/lists/*

RUN useradd --create-home --no-log-init --shell /bin/bash -G sudo,adm,root  ${user} \
    && echo ${user}:123456 | chpasswd \
    && chmod 774 /home/${user}

USER ${user}

WORKDIR /home/${user}/workspace
# 开启终端色彩
ENV TERM=xterm-256color
ENV LANG=C.UTF-8
