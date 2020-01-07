# https://github.com/docker/for-mac/issues/2155
ARG TAG=latest
FROM ataber/intel_mkl:${TAG} as base

FROM ataber/mfem:$TAG
COPY --from=base /opt/intel /opt/intel
