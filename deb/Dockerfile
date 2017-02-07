FROM ubuntu:16.04
MAINTAINER George Paraskevopoulos <georgepar.91@gmail.com>

# Tested with openfst version 1.6.1
ARG OPENFST_VERSION=1.6.1
ARG NUM_BUILD_CORES=8
ARG INSTALL_IN_CONTAINER=no
ENV OPENFST_VERSION ${OPENFST_VERSION}
ENV NUM_BUILD_CORES ${NUM_BUILD_CORES}
ENV INSTALL_IN_CONTAINER ${INSTALL_IN_CONTAINER}

RUN ln -s -f bash /bin/sh
RUN apt-get update
RUN apt-get install -y wget make gcc g++ checkinstall python-dev libz-dev

RUN wget http://www.openfst.org/twiki/pub/FST/FstDownload/openfst-${OPENFST_VERSION}.tar.gz
RUN tar -xvf openfst-${OPENFST_VERSION}.tar.gz -C /
RUN mkdir -p /openfst-deb

WORKDIR /openfst-${OPENFST_VERSION}
RUN ./configure \
        --enable-static=yes \
        --enable-shared=no \
        --with-pic=yes \
        --enable-far \
        --enable-python
RUN make -j{NUM_BUILD_CORES}
RUN checkinstall -Dy --install=${INSTALL_IN_CONTAINER}
RUN mv openfst_${OPENFST_VERSION}-1_amd64.deb /openfst-deb
VOLUME /openfst-deb

ENTRYPOINT ["bin/bash"]
