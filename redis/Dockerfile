FROM ubuntu:14.04

RUN python3 -c 'from urllib.request import urlopen; from json import loads; \
    print(loads(urlopen("http://ip-api.com/json").read().decode("utf-8" \
    ).strip())["countryCode"])' > /tmp/country

RUN test $(cat /tmp/country) = "CN" && { \
    sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list; \
    } || true

ENV REDIS_VERSION 2.8.4
ENV REDIS_APT_VERSION 2:2.8.4-2

RUN apt-get update && \
    apt-get -d \
       -o Dir::Cache=/opt \
       -o Dir::Cache::archives=redis-${REDIS_VERSION} \
       install -y redis-server=${REDIS_APT_VERSION} && \
    find /opt/redis-${REDIS_VERSION}/* -not -name '*.deb' -delete && \
    cd /opt && tar -cv redis-${REDIS_VERSION} | gzip -n > redis-${REDIS_VERSION}.tar.gz

VOLUME /mnt

CMD cp -nv /opt/redis-${REDIS_VERSION}.tar.gz /mnt
