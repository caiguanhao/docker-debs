FROM ubuntu:18.04

WORKDIR /opt

RUN apt-get update && \
    apt-get install --no-install-recommends -y curl gnupg2 ca-certificates \
    lsb-release dpkg-dev debhelper libssl-dev libpcre3-dev zlib1g-dev quilt \
    build-essential dh-systemd

RUN echo "deb-src http://nginx.org/packages/mainline/ubuntu bionic nginx" > \
    /etc/apt/sources.list.d/nginx.list && \
    apt-key adv --fetch-keys http://nginx.org/keys/nginx_signing.key && \
    apt-get update && \
    apt-get upgrade -y

RUN apt-get source nginx=1.17.6-1~bionic

ADD source.patch /opt/source.patch

RUN cd nginx-* && patch -p1 -i /opt/source.patch

RUN cd nginx-* && dpkg-buildpackage -b

VOLUME /nginx

CMD cp -v nginx_*_amd64.deb /nginx
