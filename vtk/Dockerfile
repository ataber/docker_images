FROM ataber/cmake

RUN cd /tmp && \
    wget -nv -O- http://www.vtk.org/files/release/8.1/VTK-8.1.1.tar.gz | \
    tar xz && \
    cd VTK-8.1.1 && \
    CXX=mpicxx cmake \
    -D CMAKE_BUILD_TYPE:STRING=Release \
    -D CMAKE_INSTALL_PREFIX:STRING=/usr/lib/vtk \
    -D BUILD_DOCUMENTATION:BOOL=OFF \
    -D BUILD_EXAMPLES:BOOL=OFF \
    -D BUILD_TESTING:BOOL=OFF \
    -D VTK_USE_X:BOOL=OFF \
    -D VTK_INSTALL_NO_DEVELOPMENT:BOOL=OFF \
    -D VTK_RENDERING_BACKEND:STRING=None \
    -D VTK_USE_PARALLEL:BOOL=OFF \
    -D VTK_Group_MPI:BOOL=ON \
    -D VTK_Group_StandAlone:BOOL=ON \
    -D VTK_Group_Rendering:BOOL=OFF \
    -D VTK_Group_Imaging:BOOL=OFF \
    -D VTK_Group_Qt:BOOL=OFF \
    -D VTK_Group_Tk:BOOL=OFF \
    -D VTK_Group_Web:BOOL=OFF \
    -D VTK_Group_Views:BOOL=OFF \
    -D VTK_WRAP_PYTHON=OFF \
    . && \
    make -j $(cat /proc/cpuinfo | grep processor | wc -l) VERBOSE=1 && \
    make install && \
    cd .. && rm -rf VTK-8.1.1
ENV VTK_DIR /usr/lib/vtk
