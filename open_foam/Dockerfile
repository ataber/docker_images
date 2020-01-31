ARG TAG=latest
FROM ataber/vtk:$TAG

RUN /bin/sh -c "wget -O - http://dl.openfoam.org/gpg.key | apt-key add -" && \
    add-apt-repository http://dl.openfoam.org/ubuntu
RUN apt-get update --fix-missing \
&&  apt-get upgrade -y --force-yes \
&&  DEBIAN_FRONTEND=noninteractive apt-get install -y --force-yes openfoam6 \
&&  apt-get clean \
&&  rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*
RUN echo "source /opt/openfoam6/etc/bashrc" > $HOME/bashrc

