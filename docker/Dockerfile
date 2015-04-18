FROM ubuntu:14.04

ENV DOCKER_VERSION 1.6.0

RUN echo 'deb http://get.docker.com/ubuntu docker main' > /etc/apt/sources.list.d/docker.list

RUN apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get -d -o Dir::Cache=/opt -o Dir::Cache::archives=docker-${DOCKER_VERSION} \
    install -y lxc-docker-${DOCKER_VERSION} && \
    find /opt/docker-${DOCKER_VERSION}/* -not -name '*.deb' -delete && \
    cd /opt && tar -cv docker-${DOCKER_VERSION} | gzip -n > docker-${DOCKER_VERSION}.tar.gz

VOLUME /docker

CMD cp /opt/docker-${DOCKER_VERSION}.tar.gz /docker
