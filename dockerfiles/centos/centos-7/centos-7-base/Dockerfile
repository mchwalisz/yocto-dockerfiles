# centos-7-base
# Copyright (C) 2015-2021 Intel Corporation
#
# SPDX-License-Identifier: GPL-2.0-only
#

FROM centos:centos7

RUN yum -y install epel-release centos-release-scl && \
    yum -y update && \
    yum -y install \
        gawk \
        make \
        wget \
        tar \
        bzip2 \
        gzip \
        python \
        python3 \
        unzip \
        perl \
        patch \
        diffutils \
        diffstat \
        git \
        subversion \
        cpp \
        gcc \
        gcc-c++ \
        glibc-devel \
        texinfo \
        chrpath \
        socat \
        perl-Data-Dumper \
        perl-Text-ParseWords \
        perl-Thread-Queue \
        file \
        tigervnc-server \
        xz \
        screen \
        tmux \
        sudo \
        which \
        lz4 \
        zstd && \
    cp -af /etc/skel/ /etc/vncskel/ && \
    echo "export DISPLAY=1" >>/etc/vncskel/.bashrc && \
    mkdir  /etc/vncskel/.vnc && \
    echo "" | vncpasswd -f > /etc/vncskel/.vnc/passwd && \
    chmod 0600 /etc/vncskel/.vnc/passwd && \
    groupadd -g 1000 yoctouser && \
    useradd -u 1000 -g yoctouser -m yoctouser

# The versions of gcc, tar and other tools found in Centos 7 are now too old to
# build recent Yocto Project releases. Install the buildtools tarball to
# provide the required tools.
COPY install-buildtools.sh /
RUN bash /install-buildtools.sh && \
    rm /install-buildtools.sh

COPY build-install-dumb-init.sh /
RUN  bash build-install-dumb-init.sh && \
     rm /build-install-dumb-init.sh && \
     yum -y clean all

#COPY vncserver.patch /
#RUN  patch /usr/bin/vncserver /vncserver.patch && \
#     rm /vncserver.patch

USER yoctouser
WORKDIR /home/yoctouser
CMD /bin/bash
