FROM golang:1.7

RUN dpkg --add-architecture i386 \
      && apt-get -q update \
      && apt-get -q -y upgrade \
      && DEBIAN_FRONTEND=noninteractive apt-get -y install \
        automake \
        bc \
        build-essential \
        bzr \
        cpio \
        cvs \
        gcc-multilib \
        git \
        gnupg2 \
        golang-go \
        graphviz \
        libc6:i386 \
        libncurses5-dev \
        libtool \
        locales \
        mercurial \
        p7zip-full \
        python \
        python-matplotlib \
        rsync \
        subversion \
        unzip \
        vim \
        wget \
      && rm -rf /var/lib/apt/lists/* \
      && localedef -c -f UTF-8 -i en_US en_US.UTF-8

# Install dumb init
RUN wget https://github.com/Yelp/dumb-init/releases/download/v1.2.0/dumb-init_1.2.0_amd64.deb \
      && dpkg -i dumb-init_*.deb

WORKDIR /usr/local/src
VOLUME /usr/local/src

ENTRYPOINT ["/usr/bin/dumb-init", "--"]
CMD ["/bin/bash"]
