FROM ubuntu:14.04

RUN sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/' /etc/apt/sources.list && \
    apt-get update && apt-get install -y apt-transport-https

RUN echo 'deb https://get.docker.com/ubuntu docker main' > /etc/apt/sources.list.d/docker.list

RUN apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9

ENV DOCKER_VERSION 1.6.0

RUN apt-get update && apt-get upgrade -y

RUN apt-get -d -o Dir::Cache=/opt -o Dir::Cache::archives=docker-${DOCKER_VERSION} \
    install -y lxc-docker-${DOCKER_VERSION}

RUN apt-get purge --auto-remove -y apt-transport-https

RUN apt-get -d -o Dir::Cache=/opt -o Dir::Cache::archives=docker-${DOCKER_VERSION} \
    install -y lxc-docker-${DOCKER_VERSION}

RUN find /opt/docker-${DOCKER_VERSION}/* -not -name '*.deb' -delete && \
    cd /opt && tar -cv docker-${DOCKER_VERSION} | gzip -n > docker-${DOCKER_VERSION}.tar.gz

VOLUME /docker

CMD cp /opt/docker-${DOCKER_VERSION}.tar.gz /docker
