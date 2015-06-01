FROM ubuntu:14.04

RUN python3 -c 'from urllib.request import urlopen; from json import loads; \
    print(loads(urlopen("http://ip-api.com/json").read().decode("utf-8" \
    ).strip())["countryCode"])' > /tmp/country

RUN test $(cat /tmp/country) = "CN" && { \
    sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list; \
    } || true

RUN apt-get update && \
    apt-get --no-install-recommends -d \
       -o Dir::Cache=/opt \
       -o Dir::Cache::archives=openjdk-7-jdk \
       install -y openjdk-7-jdk && \
    find /opt/openjdk-7-jdk/* -not -name '*.deb' -delete && \
    cd /opt && tar -cv openjdk-7-jdk | gzip -n > openjdk-7-jdk.tar.gz

VOLUME /openjdk

CMD cp /opt/openjdk-7-jdk.tar.gz /openjdk
