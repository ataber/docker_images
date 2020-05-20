ARG TAG=latest
FROM ataber/cmake:$TAG

RUN apt-get update --fix-missing \
&&  apt-get upgrade -y \
&&  DEBIAN_FRONTEND=noninteractive apt-get install -y \
    libtinfo5 \
&&  rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

RUN python3 -m pip install taichi
