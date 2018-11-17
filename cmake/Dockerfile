FROM ubuntu:xenial

RUN apt-get update --fix-missing \
&&  apt-get upgrade -y \
&&  apt-get install -y wget \
    software-properties-common \
    make \
    build-essential \
    clang-tidy \
    iwyu \
    cppcheck \
    libopenmpi-dev \
    openmpi-bin \
&&  rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

RUN wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add - && \
    apt-add-repository "deb http://apt.llvm.org/xenial/ llvm-toolchain-xenial-5.0 main" && \
    apt-get update --fix-missing && \
    apt-get install -y clang-5.0 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

ARG CMAKE_MAJOR_VERSION=3.12
ARG CMAKE_MINOR_VERSION=3
ARG CMAKE_VERSION=$CMAKE_MAJOR_VERSION.$CMAKE_MINOR_VERSION
RUN cd /tmp \
    && wget https://cmake.org/files/v$CMAKE_MAJOR_VERSION/cmake-$CMAKE_VERSION.tar.gz \
    && tar xf cmake-$CMAKE_VERSION.tar.gz \
    && cd cmake-$CMAKE_VERSION \
    && ./bootstrap \
    && make \
    && make install \
    && cd .. \
    && rm -rf cmake*

ENV CC clang-5.0
ENV CXX clang++-5.0
ENV MPI_C mpicc
ENV MPI_CXX mpicxx

RUN mkdir /app
WORKDIR /app
