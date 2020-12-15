ARG TAG=latest
FROM ataber/mfem_mkl:${TAG} as intel
FROM ataber/openvdb:${TAG}

# Note we need both bashrc and profile. CircleCI runs non-login shell.
# https://unix.stackexchange.com/questions/29791/bash-profile-not-sourced-when-running-su
COPY --from=intel /opt/intel /opt/intel
COPY --from=intel /etc/bashrc /etc/bashrc
COPY --from=intel /etc/profile /etc/profile
RUN cat /etc/bashrc >> ~/.bashrc
RUN cat /etc/profile >> ~/.bash_profile
