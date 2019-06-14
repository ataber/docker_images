ARG TAG=latest
FROM ataber/mfem:$TAG

RUN apt-get update --fix-missing && \
    apt-get -y upgrade && \
    apt-get install -y git build-essential make gfortran wget cpio && rm -rf /var/lib/apt/lists/*

ARG MKL_VER=2019.3.199
ARG MKL_NAME=l_mkl_$MKL_VER
ARG MKL_URL=http://registrationcenter-download.intel.com/akdlm/irc_nas/tec/15275/${MKL_NAME}.tgz
RUN cd /tmp && \
  wget -q $MKL_URL && \
  tar -xzf ${MKL_NAME}.tgz && \
  cd $MKL_NAME && \
  sed -i 's/ACCEPT_EULA=decline/ACCEPT_EULA=accept/g' silent.cfg && \
  sed -i 's/ARCH_SELECTED=ALL/ARCH_SELECTED=INTEL64/g' silent.cfg && \
  sed -i 's/COMPONENTS=DEFAULTS/COMPONENTS=;intel-comp-l-all-vars__noarch;intel-comp-nomcu-vars__noarch;intel-openmp__x86_64;intel-tbb-libs__x86_64;intel-mkl-common__noarch;intel-mkl-installer-license__noarch;intel-mkl-core__x86_64;intel-mkl-core-rt__x86_64;intel-mkl-doc__noarch;intel-mkl-doc-ps__noarch;intel-mkl-gnu__x86_64;intel-mkl-gnu-rt__x86_64;intel-mkl-common-ps__noarch;intel-mkl-core-ps__x86_64;intel-mkl-common-c__noarch;intel-mkl-core-c__x86_64;intel-mkl-common-c-ps__noarch;intel-mkl-tbb__x86_64;intel-mkl-tbb-rt__x86_64;intel-mkl-gnu-c__x86_64;intel-mkl-common-f__noarch;intel-mkl-core-f__x86_64;intel-mkl-gnu-f-rt__x86_64;intel-mkl-gnu-f__x86_64;intel-mkl-f95-common__noarch;intel-mkl-f__x86_64;intel-mkl-psxe__noarch;intel-psxe-common__noarch;intel-psxe-common-doc__noarch;intel-compxe-pset/g' silent.cfg && \
  ./install.sh -s silent.cfg && \
  cd .. && rm -rf * && \
  rm -rf /opt/intel/.*.log /opt/intel/compilers_and_libraries_${MKL_VER}/licensing && \
  echo "/opt/intel/mkl/lib/intel64" >> /etc/ld.so.conf.d/intel.conf && \
  ldconfig && \
  touch /etc/bashrc && \
  echo "source /opt/intel/mkl/bin/mklvars.sh intel64" >> /etc/bashrc && \
  echo "source /opt/intel/mkl/bin/mklvars.sh intel64" >> /etc/bash.bashrc
