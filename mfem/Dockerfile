ARG TAG=latest
FROM ataber/mkl_vtk:$TAG

# Update apt and install apt dependencies
RUN apt-get update --fix-missing \
&&  apt-get upgrade -y --force-yes \
&&  apt-get install -y --force-yes \
    bzip2 \
    gfortran \
    unzip \
    wget \
    libopenmpi-dev \
    openmpi-bin \
    git \
    m4 \
    pkg-config \
    libgmp3-dev \
    libmpfr-dev \
&&  apt-get clean \
&&  rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

# Build and install SuiteSparse solvers needed for mfem
ENV SuiteSparse_DIR /opt/suitesparse
RUN export CXXFLAGS="$CXXFLAGS -fPIC" && \
    export CFLAGS="$CFLAGS -fPIC" && \
    cd /tmp && \
    git clone https://github.com/DrTimothyAldenDavis/SuiteSparse && \
    cd SuiteSparse && \
    make  library -j $(cat /proc/cpuinfo | grep processor | wc -l) && \
    make INSTALL=$SuiteSparse_DIR install && \
    rm -rf /tmp/SuiteSparse

# Build and install METIS
ENV METIS_DIR /opt/metis
RUN export CXXFLAGS="$CXXFLAGS -fPIC" && \
    export CFLAGS="$CFLAGS -fPIC" && \
    cd /tmp && \
    git clone https://github.com/scivision/METIS.git && \
    cd METIS && \
    mkdir build && \
    cd build && \
    cmake .. \
    -DCMAKE_INSTALL_PREFIX=$METIS_DIR &&\
    make -j $(cat /proc/cpuinfo | grep processor | wc -l) && \
    make install && \
    rm -rf /tmp/METIS

# Build and install HYPRE
ENV HYPRE_DIR /opt/hypre
run export CXXFLAGS="$CXXFLAGS -fPIC" && \
    export CFLAGS="$CFLAGS -fPIC" && \
    cd /tmp && \
    git clone https://github.com/hypre-space/hypre.git && \
    cd /tmp/hypre/src/cmbuild && \
    CXX=mpicxx \
    cmake .. && \
    make -j $(cat /proc/cpuinfo | grep processor | wc -l) && \
    make install && \
    cp -r /tmp/hypre/src/hypre /opt && \
    rm -rf /tmp/hypre

# Build and install MFEM
ENV MFEM_DIR /opt/mfem
RUN export CXXFLAGS="$CXXFLAGS -fPIC" && \
    export CFLAGS="$CFLAGS -fPIC" && \
    cd /tmp && \
    git clone https://github.com/mfem/mfem.git && \
    cd mfem && \
    mkdir build && \
    cd build && \
    CXX=mpicxx \
    cmake .. \
        -DCMAKE_INSTALL_PREFIX=$MFEM_DIR \
        -DMFEM_USE_MPI=ON \
        -DMFEM_USE_SUITESPARSE=ON \
        -DCMAKE_POSITION_INDEPENDENT_CODE=ON \
        -DMFEM_USE_PETSC=OFF \
        -DBUILD_SHARED_LIBS=OFF \
        -DMFEM_THREAD_SAFE=ON \
        -DMFEM_USE_METIS=1 && \
    make -j $(cat /proc/cpuinfo | grep processor | wc -l) && \
    make install && \
    rm -rf /tmp/mfem

