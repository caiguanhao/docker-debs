FROM ubuntu:19.10

RUN apt-get update

RUN apt-get -d -o Dir::Cache=/opt -o Dir::Cache::archives=redis-server \
    install --no-install-recommends -y redis-server

RUN find /opt/redis-server/* -not -name '*.deb' -delete && \
    cd /opt && tar -cv redis-server | gzip -n > redis-server-5.tar.gz

VOLUME /redis

CMD cp -nv /opt/redis-server-5.tar.gz /redis
