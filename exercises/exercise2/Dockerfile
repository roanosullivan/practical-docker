# OR Use ARG to set it at build time
ARG version=21.04
FROM ubuntu:${version}

RUN apt-get   update -y \
  && apt-get install -y jq iputils-ping

