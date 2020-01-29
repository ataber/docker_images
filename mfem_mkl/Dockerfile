# https://github.com/docker/for-mac/issues/2155
ARG TAG=latest
FROM ataber/intel_mkl:${TAG} as intel

FROM ataber/mfem:${TAG}
COPY --from=intel /opt/intel /opt/intel
COPY --from=intel /etc/bashrc /etc/bashrc
RUN cat /etc/bashrc >> ~/.bashrc
