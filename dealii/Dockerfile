FROM ataber/trilinos

RUN apt-get update --fix-missing \
&&  apt-get upgrade -y --force-yes \
&&  apt-get install -y --force-yes \
    git \
    ninja-build \
    numdiff \
    pkg-config \
&&  apt-get clean \
&&  rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

# dealii
ARG VER=master
ARG BUILD_TYPE=Release
ARG INSTALL_DIR=/usr/lib
RUN cd /tmp && \
    git clone https://github.com/dealii/dealii.git dealii-$VER-src && \
    cd dealii-$VER-src && \
    git checkout $VER && \
    mkdir build && cd build && \
    CXX=mpicxx cmake -DCMAKE_INSTALL_PREFIX=$INSTALL_DIR \
          -DCMAKE_BUILD_TYPE=$BUILD_TYPE \
          -GNinja \
          ../ && \
    ninja library && \
    ninja install && \
    cd /tmp && \
    rm -rf dealii-$VER-src

ENV DEAL_II_DIR $INSTALL_DIR

