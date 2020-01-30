# https://github.com/docker/for-mac/issues/2155
ARG TAG=latest
FROM ataber/intel_mkl:${TAG} as intel

FROM ataber/vtk:${TAG}
COPY --from=intel /opt/intel /opt/intel
# Note we need both bashrc and profile. CircleCI runs non-login shell.
# https://unix.stackexchange.com/questions/29791/bash-profile-not-sourced-when-running-su
COPY --from=intel /etc/bashrc /etc/bashrc
COPY --from=intel /etc/profile /etc/profile
