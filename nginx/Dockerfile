FROM ubuntu:16.04

WORKDIR /opt

RUN echo "deb-src http://nginx.org/packages/mainline/ubuntu xenial nginx" > \
    /etc/apt/sources.list.d/nginx.list && \
    apt-key adv --fetch-keys http://nginx.org/keys/nginx_signing.key && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y dh-systemd dpkg-dev debhelper zlib1g-dev quilt lsb-release \
    libssl-dev libpcre3-dev libexpat-dev libgd-dev libgeoip-dev libluajit-5.1-dev libmhash-dev libpam0g-dev libperl-dev libxslt1-dev

RUN apt-get source nginx=1.10.0-0ubuntu0.16.04.4

RUN curl -Ls https://github.com/vozlt/nginx-module-vts/archive/v0.1.11.tar.gz | tar xfvz -

ADD source.patch /opt/source.patch

RUN cd nginx-* && patch -p1 -i /opt/source.patch && dpkg-buildpackage -b

VOLUME /nginx

CMD cp -v nginx_*_amd64.deb /nginx
