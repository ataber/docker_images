ARG TAG=latest
FROM ataber/trilinos:$TAG

RUN apt-get update --fix-missing \
&&  apt-get upgrade -y --force-yes \
&&  apt-get install -y --force-yes \
    git \
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
    CXX=mpicxx cmake \
        -DCMAKE_INSTALL_PREFIX=$INSTALL_DIR \
        -DBUILD_SHARED_LIBS=OFF \
        -DDEAL_II_WITH_MPI=ON \
        -DDEAL_II_WITH_PETSC=ON \
        -DDEAL_II_WITH_SLEPC=ON \
        -DCMAKE_BUILD_TYPE=$BUILD_TYPE \
        ../ && \
    make -j $(cat /proc/cpuinfo | grep processor | wc -l) library && \
    make install && \
    cd /tmp && \
    rm -rf dealii-$VER-src

ENV DEAL_II_DIR $INSTALL_DIR/dealii
