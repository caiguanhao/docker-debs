FROM ubuntu:16.04

RUN apt-get update && apt-get install -y apt-transport-https ca-certificates curl software-properties-common

RUN curl -fsSL https://apt.dockerproject.org/gpg | apt-key add -

RUN add-apt-repository "deb https://apt.dockerproject.org/repo/ ubuntu-$(lsb_release -cs) main"

RUN apt-get update && apt-get upgrade -y

ENV DOCKER_VERSIONS 1.13.1

RUN for DOCKER_VERSION in $DOCKER_VERSIONS; do \
    apt-get -d -o Dir::Cache=/opt -o Dir::Cache::archives=docker-${DOCKER_VERSION} \
    install --no-install-recommends -y docker-engine=${DOCKER_VERSION}-0~ubuntu-xenial; \
    done

RUN for DOCKER_VERSION in $DOCKER_VERSIONS; do \
    find /opt/docker-${DOCKER_VERSION}/* -not -name '*.deb' -delete && \
    cd /opt && tar -cv docker-${DOCKER_VERSION} | gzip -n > docker-${DOCKER_VERSION}.tar.gz; \
    done

VOLUME /docker

CMD cp -nv /opt/docker-*.tar.gz /docker
