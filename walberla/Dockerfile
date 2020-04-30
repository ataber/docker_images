ARG TAG=latest
FROM ataber/vtk:$TAG

RUN apt-get update --fix-missing \
&&  apt-get upgrade -y --force-yes \
&&  apt-get install -y --force-yes \
    git \
    libopenmpi-dev \
    openmpi-bin \
&&  apt-get clean \
&&  rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

RUN cd /tmp && \
    git clone https://i10git.cs.fau.de/walberla/walberla && \
    cd walberla && \
    mkdir build && cd build && \
    cmake \
        -DCMAKE_INSTALL_PREFIX=/usr/lib \
        -DWALBERLA_BUILD_TUTORIALS=OFF \
        -DWALBERLA_BUILD_WITH_MPI=ON \
        -DWALBERLA_BUILD_WITH_OPENMP=ON \
        -DWALBERLA_BUILD_TESTS=OFF \
        -DWALBERLA_BUILD_BENCHMARKS=OFF \
        -DWALBERLA_BUILD_WITH_PYTHON_MODULE=OFF \
        .. && \
    make -j $(cat /proc/cpuinfo | grep processor | wc -l) && \
    make install && \
    cd /tmp && \
    rm -rf walberla
