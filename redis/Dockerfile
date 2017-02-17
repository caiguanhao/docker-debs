FROM ubuntu:16.04

WORKDIR /opt

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y dpkg-dev debhelper libssl-dev libpcre3-dev zlib1g-dev curl

RUN curl -Ls https://github.com/lamby/pkg-redis/archive/debian/sid.tar.gz | tar xfvz -

RUN apt-get install -y dh-systemd libjemalloc-dev tcl && apt-get download libjemalloc1

RUN cd pkg-redis-debian-sid && DEB_BUILD_OPTIONS=nocheck dpkg-buildpackage -b

RUN mkdir -p redis-3.2.8 && cp *.deb redis-3.2.8 && tar -cv redis-3.2.8 | gzip -n > redis-3.2.8.tar.gz

VOLUME /redis

CMD cp -nv /opt/redis-3.2.8.tar.gz /redis
