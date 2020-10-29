FROM ubuntu:20.04

RUN apt-get update && \
    apt-get -d -o Dir::Cache=/opt -o Dir::Cache::archives=memcached \
    install -y memcached && \
    find /opt/memcached/* -not -name '*.deb' -delete && \
    cd /opt && tar -cv memcached | gzip -n > memcached.tar.gz

VOLUME /memcached

CMD cp -nv /opt/memcached.tar.gz /memcached
