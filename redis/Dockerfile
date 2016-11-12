FROM ubuntu:14.04

WORKDIR /opt

RUN python3 -c 'from urllib.request import urlopen; from json import loads; \
    print(loads(urlopen("http://ip-api.com/json").read().decode("utf-8" \
    ).strip())["countryCode"])' > /tmp/country

RUN test $(cat /tmp/country) = "CN" && { \
    sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list; \
    } || true

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y dpkg-dev debhelper libssl-dev libpcre3-dev zlib1g-dev curl

RUN curl -Ls https://github.com/lamby/pkg-redis/archive/debian/sid.tar.gz | tar xfvz -

RUN apt-get install -y dh-systemd libjemalloc-dev tcl && apt-get download libjemalloc1

RUN cd pkg-redis-debian-sid && DEB_BUILD_OPTIONS=nocheck dpkg-buildpackage -b

RUN mkdir -p redis-3.2.5 && cp *.deb redis-3.2.5 && tar -cv redis-3.2.5 | gzip -n > redis-3.2.5.tar.gz

VOLUME /redis

CMD cp -nv /opt/redis-3.2.5.tar.gz /redis
