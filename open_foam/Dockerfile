ARG TAG=latest
FROM ataber/vtk:$TAG

ENV OPEN_FOAM_VERSION 7
RUN /bin/sh -c "wget -O - http://dl.openfoam.org/gpg.key | apt-key add -" && \
    add-apt-repository http://dl.openfoam.org/ubuntu
RUN DEBIAN_FRONTEND=noninteractive apt-get update --fix-missing \
&&  apt-get upgrade -y --force-yes \
&&  apt-get install -y --force-yes openfoam$OPEN_FOAM_VERSION \
&&  apt-get clean \
&&  rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*
RUN echo "source /opt/openfoam$OPEN_FOAM_VERSION/etc/bashrc" > $HOME/bashrc

