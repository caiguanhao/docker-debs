FROM ubuntu:20.04

RUN apt-get update && apt-get upgrade -y && apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

RUN echo "deb-src http://nginx.org/packages/ubuntu/ focal nginx" > \
    /etc/apt/sources.list.d/nginx.list && \
    apt-key adv --fetch-keys http://nginx.org/keys/nginx_signing.key && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install --no-install-recommends -y \
    lsb-release dpkg-dev debhelper libssl-dev libpcre3-dev zlib1g-dev quilt \
    build-essential dh-systemd

RUN apt-get source nginx=1.18.0-1~focal

ADD source.patch /opt/source.patch

RUN cd nginx-* && patch -p1 -i /opt/source.patch && dpkg-buildpackage -b

VOLUME /nginx

CMD cp -v nginx_*_amd64.deb /nginx
