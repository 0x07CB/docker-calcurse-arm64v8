FROM arm64v8/debian:stable
# ##############################################################################
# # Dockerfile to build a calcurse image for arm64v8 architecture with debian. #
# ##############################################################################
LABEL maintainer="0x07cb"
# GITEA REPOSITORY: 
# GITHUB REPOSITORY: 
# ##############################################################################
# Install dependencies
RUN apt update \
    && apt install -y \
    wget \
    make \
    cmake \
    gcc \
    ninja-build \
    build-essential \
    tar \
    gzip \
    libncurses-dev

USER root
WORKDIR /tmp
RUN wget https://calcurse.org/files/calcurse-4.8.1.tar.gz -O /tmp/calcurse-4.8.1.tar.gz \
        && wget https://calcurse.org/files/calcurse-4.8.1.tar.gz.md5sum -O /tmp/calcurse-4.8.1.tar.gz.md5sum 

#md5sum -c /tmp/calcurse-4.8.1.tar.gz.md5sum | grep "OK" && tar -xvf /tmp/calcurse-4.8.1.tar.gz || echo "Download failed" && exit 1

RUN tar -xvf /tmp/calcurse-4.8.1.tar.gz \
    && rm -rf /tmp/calcurse-4.8.1.tar.gz \
    && rm -rf /tmp/calcurse-4.8.1.tar.gz.md5sum
WORKDIR /tmp/calcurse-4.8.1
RUN ./configure \
    && make -j$(nproc) \
    && make install

WORKDIR /tmp/
RUN rm -rf /tmp/calcurse-4.8.1

WORKDIR /root
# Nettoie le cache APT et supprime les paquets inutiles
RUN apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

USER root
WORKDIR /root

ENTRYPOINT ["/usr/local/bin/calcurse"]
# Written by 0x07cb ( Rick Sanchez )
# ##############################################################################
# P.S.: That can be better, more optimized, more secure, more everything... if you re-write it to use alpine or scratch...
#       I'm not responsible for any damage caused by this script.
#       You are running this script at your own risk.
#       Yes I now, I'm a genius. Thank you for noticing.
#       But I don't care.
# ##############################################################################
