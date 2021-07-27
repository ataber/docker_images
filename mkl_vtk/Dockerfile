# https://github.com/docker/for-mac/issues/2155
ARG TAG=latest
FROM ataber/intel_mkl:${TAG} as intel

FROM ataber/vtk:${TAG}
COPY --from=intel /opt/intel /opt/intel

# Note we need both bashrc and profile. CircleCI runs non-login shell.
# https://unix.stackexchange.com/questions/29791/bash-profile-not-sourced-when-running-su
# We need the /etc/ paths so that bash scripts will get intel variables
# I'm unclear if we also need to the files in ~, but I didn't want to spend the time checking
RUN touch /etc/bashrc && \
    touch /etc/profile && \
    touch ~/.bash_profile && \
    touch ~/bashrc && \
    echo "source /opt/intel/mkl/bin/mklvars.sh intel64" >> /etc/bashrc && \
    echo "source /opt/intel/mkl/bin/mklvars.sh intel64" >> /etc/profile && \
    echo "source /opt/intel/mkl/bin/mklvars.sh intel64" >> ~/.bashrc && \
    echo "source /opt/intel/mkl/bin/mklvars.sh intel64" >> ~/.bash_profile
