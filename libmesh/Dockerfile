ARG TAG=latest
FROM ataber/slepc:$TAG

RUN apt-get update --fix-missing \
&&  apt-get install -y --force-yes \
    git \
    m4 \
    pkg-config \
    libproj-dev \
&&  apt-get clean \
&&  rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

ENV LIBMESH_DIR /opt/libmesh
RUN cd /tmp && \
    git clone https://github.com/libMesh/libmesh.git && \
    cd libmesh && \
    git submodule update --init && \
    mkdir build && \
    cd build && \
    ../configure --with-methods="opt" \
                 --prefix=$LIBMESH_DIR \
                 --disable-boost \
                 --disable-metaphysicl \
                 --enable-petsc \
                 --enable-slepc \
                 --enable-vtk \
                 --with-vtk-include=$VTK_DIR/include/vtk-$VTK_MAJOR_VERSION.$VTK_MINOR_VERSION \
                 --with-vtk-lib=$VTK_DIR/lib \
                 --disable-eigen \
                 --with-cxx=mpicxx \
                 --with-metis=PETSc && \
    make -j $(cat /proc/cpuinfo | grep processor | wc -l) && \
    make install && \
    cd /tmp && rm -rf libmesh
