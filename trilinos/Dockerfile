FROM ataber/slepc

RUN apt-get update --fix-missing \
&&  apt-get upgrade -y --force-yes \
&&  apt-get install -y --force-yes \
    gfortran \
    gsl-bin \
    libblas-dev \
    libgsl0-dev \
    liblapack-dev \
    libsuitesparse-dev \
    libtbb-dev \
    libtbb2 \
    numdiff \
    python \
    wget \
    libopenmpi-dev \
    openmpi-bin \
&&  apt-get clean \
&&  rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

# Make open mpi use clang
ENV OMPI_CC clang-5.0
ENV OMPI_CXX clang++-5.0

#Build Trilinos
ENV TRILINOS_VERSION 12-12-1
RUN cd /tmp && \
    wget https://github.com/trilinos/Trilinos/archive/trilinos-release-$TRILINOS_VERSION.tar.gz && \
    tar xfz trilinos-release-$TRILINOS_VERSION.tar.gz && \
    mkdir Trilinos-trilinos-release-$TRILINOS_VERSION/build && \
    cd Trilinos-trilinos-release-$TRILINOS_VERSION/build && \
    cmake \
     -D BUILD_SHARED_LIBS=OFF \
     -D CMAKE_BUILD_TYPE=RELEASE \
     -D CMAKE_CXX_FLAGS="-O3" \
     -D CMAKE_C_FLAGS="-O3" \
     -D CMAKE_FORTRAN_FLAGS="-O5" \
     -D CMAKE_INSTALL_PREFIX:PATH=/usr/lib/trilinos-$TRILINOS_VERSION \
     -D CMAKE_VERBOSE_MAKEFILE=FALSE \
     -D TPL_ENABLE_Boost=OFF \
     -D TPL_ENABLE_MPI=ON \
     -D TPL_ENABLE_Netcdf:BOOL=OFF \
     -D TrilinosFramework_ENABLE_MPI:BOOL=ON \
     -D Trilinos_ASSERT_MISSING_PACKAGES:BOOL=OFF \
     -D Trilinos_ENABLE_ALL_OPTIONAL_PACKAGES:BOOL=OFF \
     -D Trilinos_ENABLE_ALL_PACKAGES:BOOL=OFF \
     -D Trilinos_ENABLE_Amesos:BOOL=OFF \
     -D Trilinos_ENABLE_AztecOO:BOOL=ON \
     -D Trilinos_ENABLE_Epetra:BOOL=ON \
     -D Trilinos_ENABLE_EpetraExt:BOOL=ON \
     -D Trilinos_ENABLE_Ifpack:BOOL=ON \
     -D Trilinos_ENABLE_Jpetra:BOOL=ON \
     -D Trilinos_ENABLE_Kokkos:BOOL=ON \
     -D Trilinos_ENABLE_Komplex:BOOL=OFF \
     -D Trilinos_ENABLE_ML:BOOL=ON \
     -D Trilinos_ENABLE_MOOCHO:BOOL=ON \
     -D Trilinos_ENABLE_MueLu:BOOL=ON \
     -D Trilinos_ENABLE_OpenMP:BOOL=OFF \
     -D Trilinos_ENABLE_Piro:BOOL=ON \
     -D Trilinos_ENABLE_Rythmos:BOOL=OFF \
     -D Trilinos_ENABLE_STK:BOOL=OFF \
     -D Trilinos_ENABLE_Sacado=ON \
     -D Trilinos_ENABLE_TESTS:BOOL=OFF \
     -D Trilinos_ENABLE_Stratimikos=ON \
     -D Trilinos_ENABLE_Teuchos:BOOL=ON \
     -D Trilinos_ENABLE_Thyra:BOOL=ON \
     -D Trilinos_ENABLE_Tpetra:BOOL=ON \
     -D Trilinos_ENABLE_NOX:BOOL=ON \
     -D NOX_ENABLE_Epetra:BOOL=ON \
     -D NOX_ENABLE_EpetraExt:BOOL=ON \
     -D NOX_ENABLE_LAPACK:BOOL=ON \
     -D Trilinos_ENABLE_TrilinosCouplings:BOOL=ON \
     -D Trilinos_EXTRA_LINK_FLAGS="-lgfortran" \
     -D Trilinos_VERBOSE_CONFIGURE=TRUE \
     .. && \
   make -j $(cat /proc/cpuinfo | grep processor | wc -l) && make install && \
   cd /tmp && \
   rm -rf Trilinos-trilinos-release-* &&\
   rm -rf trilinos-release-*
ENV TRILINOS_DIR /usr/lib/trilinos-$TRILINOS_VERSION

