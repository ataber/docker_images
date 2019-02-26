ARG TAG=latest
FROM ataber/vtk:$TAG

RUN apt-get update --fix-missing \
&&  apt-get upgrade -y --force-yes \
&&  apt-get install -y --force-yes \
    flex \
    git-core \
    bison \
    zlib1g-dev \
    libboost-system-dev \
    libboost-thread-dev \
    libopenmpi-dev \
    openmpi-bin \
    gnuplot \
    libreadline-dev \
    libncurses-dev \
    libxt-dev \
    mpich \
&&  apt-get clean \
&&  rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

ARG HOME_SCRATCH=$HOME
# Hack to get OpenFOAM acknowledging correct directory.
ENV HOME /tmp
RUN mkdir -p /tmp/OpenFOAM && cd /tmp/OpenFOAM && \
    git clone https://github.com/OpenFOAM/OpenFOAM-dev.git && \
    git clone https://github.com/OpenFOAM/ThirdParty-dev.git && \
    echo "source /tmp/OpenFOAM-dev/etc/bashrc" >> ~/.bashrc && \
    /bin/sh /tmp/OpenFOAM/OpenFOAM-dev/etc/bashrc && \
    (cd ThirdParty-dev && ./Allwmake -j $(cat /proc/cpuinfo | grep processor | wc -l)) && \
    (cd OpenFOAM-dev && ./Allwmake -j $(cat /proc/cpuinfo | grep processor | wc -l)) && \
    cd /tmp && rm -rf OpenFOAM
ENV HOME $HOME_SCRATCH
