FROM ubuntu:14.04

RUN python3 -c 'from urllib.request import urlopen; from json import loads; \
    print(loads(urlopen("http://ip-api.com/json").read().decode("utf-8" \
    ).strip())["countryCode"])' > /tmp/country

RUN test $(cat /tmp/country) = "CN" && { \
    sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list; \
    } || true

RUN echo 'deb http://repo.varnish-cache.org/ubuntu/ precise varnish-4.0' > /etc/apt/sources.list.d/varnish-cache.list

ADD key /tmp/key

RUN apt-key add /tmp/key

RUN apt-get update && \
    apt-get -d -o Dir::Cache=/opt -o Dir::Cache::archives=varnish \
    install -y varnish && \
    find /opt/varnish/* -not -name '*.deb' -delete && \
    cd /opt && tar -cv varnish | gzip -n > varnish.tar.gz

VOLUME /varnish

CMD cp /opt/varnish.tar.gz /varnish
