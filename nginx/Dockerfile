FROM ubuntu:14.04

WORKDIR /opt

RUN python3 -c 'from urllib.request import urlopen; from json import loads; \
    print(loads(urlopen("http://ip-api.com/json").read().decode("utf-8" \
    ).strip())["countryCode"])' > /tmp/country

RUN test $(cat /tmp/country) = "CN" && { \
    sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list; \
    } || true

RUN echo "deb-src http://nginx.org/packages/mainline/ubuntu trusty nginx" > \
    /etc/apt/sources.list.d/nginx.list && \
    python3 -c 'from urllib.request import urlopen; \
    print(urlopen("http://nginx.org/keys/nginx_signing.key").read().decode("utf-8"))' | \
    apt-key add - && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y dpkg-dev debhelper libssl-dev libpcre3-dev zlib1g-dev

RUN apt-get source nginx

ADD source.patch /opt/source.patch

RUN cd nginx-* && patch -p1 -i /opt/source.patch && dpkg-buildpackage -b

VOLUME /nginx

CMD cp -nv nginx_*_amd64.deb /nginx
