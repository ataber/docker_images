FROM ataber/petsc

#slepc
ENV SLEPC_VERSION 3.10.1
RUN cd /tmp && \
    wget http://slepc.upv.es/download/distrib/slepc-$SLEPC_VERSION.tar.gz \
    -O slepc-$SLEPC_VERSION.tar.gz && \
    tar xfz slepc-$SLEPC_VERSION.tar.gz && rm -f slepc-$SLEPC_VERSION.rag.gz && \
    cd slepc-$SLEPC_VERSION && \
    ./configure --prefix=/usr/lib/slepc-$SLEPC_VERSION && \
    make SLEPC_DIR=`pwd` -j $(cat /proc/cpuinfo | grep processor | wc -l) && make SLEPC_DIR=`pwd` install && \
    cd /tmp && rm -rf slepc-$SLEPC_VERSION*

ENV SLEPC_DIR /usr/lib/slepc-$SLEPC_VERSION
