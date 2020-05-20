FROM ubuntu:20.04

RUN apt-get update --fix-missing \
&&  apt-get upgrade -y \
&&  DEBIAN_FRONTEND=noninteractive apt-get install -y \
    wget \
    software-properties-common \
    make \
    build-essential \
    libssl-dev \
    clang-tidy \
    iwyu \
    cppcheck \
    doxygen \
    graphviz \
    libopenmpi-dev \
    openmpi-bin \
    google-perftools \
    python3.7 \
    python3-dev \
    python3-distutils \
    python3-pip \
    python3-sphinx \
    libgoogle-perftools-dev \
    lldb \
    valgrind \
&&  rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

RUN wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add - && \
    apt-add-repository "deb http://apt.llvm.org/bionic/ llvm-toolchain-bionic-9 main" && \
    apt-get update --fix-missing && \
    apt-get install -y clang-9 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

ARG CMAKE_MAJOR_VERSION=3.16
ARG CMAKE_MINOR_VERSION=2
ARG CMAKE_VERSION=$CMAKE_MAJOR_VERSION.$CMAKE_MINOR_VERSION

RUN cd /tmp \
    && wget https://cmake.org/files/v$CMAKE_MAJOR_VERSION/cmake-$CMAKE_VERSION.tar.gz \
    && tar xf cmake-$CMAKE_VERSION.tar.gz \
    && cd cmake-$CMAKE_VERSION \
    && ./bootstrap \
    && make -j $(cat /proc/cpuinfo | grep processor | wc -l) \
    && make install \
    && cd .. \
    && rm -rf cmake*

ENV CC clang-9
ENV CXX clang++-9
ENV MPI_C mpicc
ENV MPI_CXX mpicxx

RUN mkdir /app
WORKDIR /app
