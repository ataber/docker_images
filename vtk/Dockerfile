ARG TAG=latest
FROM ataber/cmake:$TAG

ENV VTK_MAJOR_VERSION=8
ENV VTK_MINOR_VERSION=2
ENV VTK_PATCH_VERSION=0
ENV VTK_VERSION=$VTK_MAJOR_VERSION.$VTK_MINOR_VERSION.$VTK_PATCH_VERSION

RUN cd /tmp && \
    wget -nv -O- http://www.vtk.org/files/release/$VTK_MAJOR_VERSION.$VTK_MINOR_VERSION/VTK-$VTK_VERSION.tar.gz | \
    tar xz && \
    cd VTK-$VTK_VERSION && \
    mkdir build && \
    cd build && \
    CXX=mpicxx cmake \
    -D CMAKE_BUILD_TYPE:STRING=Release \
    -D CMAKE_INSTALL_PREFIX:STRING=/usr/lib/vtk \
    -D CMAKE_POSITION_INDEPENDENT_CODE=ON \
    -D BUILD_DOCUMENTATION:BOOL=OFF \
    -D BUILD_EXAMPLES:BOOL=OFF \
    -D BUILD_TESTING:BOOL=OFF \
    -D BUILD_SHARED_LIBS:BOOL=OFF \
    -D VTK_USE_X:BOOL=OFF \
    -D VTK_INSTALL_NO_DEVELOPMENT:BOOL=OFF \
    -D VTK_RENDERING_BACKEND:STRING=None \
    -D VTK_USE_PARALLEL:BOOL=ON \
    -D VTK_Group_MPI:BOOL=ON \
    -D VTK_Group_StandAlone:BOOL=ON \
    -D VTK_Group_Rendering:BOOL=OFF \
    -D VTK_Group_Imaging:BOOL=OFF \
    -D VTK_Group_Qt:BOOL=OFF \
    -D VTK_Group_Tk:BOOL=OFF \
    -D VTK_Group_Web:BOOL=OFF \
    -D VTK_Group_Views:BOOL=OFF \
    -D VTK_WRAP_PYTHON=OFF \
    .. && \
    make -j $(cat /proc/cpuinfo | grep processor | wc -l) VERBOSE=1 && \
    make install && \
    cd ../.. && rm -rf VTK-$VTK_VERSION
ENV VTK_DIR /usr/lib/vtk
