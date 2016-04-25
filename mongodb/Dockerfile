FROM ubuntu:14.04

RUN python3 -c 'from urllib.request import urlopen; from json import loads; \
    print(loads(urlopen("http://ip-api.com/json").read().decode("utf-8" \
    ).strip())["countryCode"])' > /tmp/country

RUN test $(cat /tmp/country) = "CN" && { \
    sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list; \
    } || true

RUN echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | \
    tee /etc/apt/sources.list.d/mongodb.list && \
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10 && \
    apt-get update

RUN apt-get --no-install-recommends -d \
       -o Dir::Cache=/opt \
       -o Dir::Cache::archives=mongodb-2.6.9 \
       install -y mongodb-org=2.6.9 \
       mongodb-org-server=2.6.9 \
       mongodb-org-shell=2.6.9 \
       mongodb-org-mongos=2.6.9 \
       mongodb-org-tools=2.6.9

RUN find /opt/mongodb-2.6.9/* -not -name '*.deb' -delete && \
    cd /opt && tar -cv mongodb-2.6.9 | gzip -n > mongodb-2.6.9.tar.gz

VOLUME /mongodb

CMD cp -nv /opt/mongodb-2.6.9.tar.gz /mongodb
