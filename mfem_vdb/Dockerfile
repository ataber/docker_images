ARG TAG=latest
FROM ataber/mfem:${TAG}

RUN echo "deb http://cz.archive.ubuntu.com/ubuntu eoan main universe" | tee -a  /etc/apt/sources.list
&& apt-get update --fix-missing \
&&  apt-get upgrade -y --force-yes \
&&  DEBIAN_FRONTEND=noninteractive apt-get install -y \
    build-essential \
    libboost-iostreams-dev \
    libboost-system-dev \
    libtbb-dev \
    libilmbase-dev \
    libopenexr-dev \
&&  apt-get clean \
&&  rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

RUN cd /tmp && \
    git clone https://github.com/Blosc/c-blosc.git && \
    cd c-blosc && \
    git checkout tags/v1.5.0 -b v1.5.0 && \
    mkdir build && \
    cd build && \
    cmake .. && \
    make -j4 && \
    make install && \
    cd ../.. && \
    rm -rf c-blosc

RUN cd /tmp && \
    git clone https://github.com/AcademySoftwareFoundation/openvdb.git && \
    cd openvdb && \
    git checkout tags/v8.1.0 -b v8.1.0 && \
    mkdir build && \
    cd build && \
    cmake .. && \
    make -j4 && \
    make install && \
    cd ../.. && \
    rm -rf openvdb
