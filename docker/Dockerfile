FROM ubuntu:20.04

RUN apt-get update && apt-get upgrade -y && apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -

RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

ENV DOCKER_VERSIONS 19.03.13

RUN for DOCKER_VERSION in $DOCKER_VERSIONS; do \
    apt-get -d -o Dir::Cache=/opt -o Dir::Cache::archives=docker-${DOCKER_VERSION} \
    install --no-install-recommends -y docker-ce=5:${DOCKER_VERSION}~3-0~ubuntu-focal docker-ce-cli=5:${DOCKER_VERSION}~3-0~ubuntu-focal containerd.io; \
    done

RUN for DOCKER_VERSION in $DOCKER_VERSIONS; do \
    find /opt/docker-${DOCKER_VERSION}/* -not -name '*.deb' -delete && \
    cd /opt && tar -cv docker-${DOCKER_VERSION} | gzip -n > docker-${DOCKER_VERSION}.tar.gz; \
    done

VOLUME /docker

CMD cp -nv /opt/docker-*.tar.gz /docker
