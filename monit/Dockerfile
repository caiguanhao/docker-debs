FROM ubuntu:20.04

RUN apt-get update

RUN apt-get -d -o Dir::Cache=/opt -o Dir::Cache::archives=monit \
    install --no-install-recommends -y monit

RUN find /opt/monit/* -not -name '*.deb' -delete && \
    cd /opt && tar -cv monit | gzip -n > monit.tar.gz

VOLUME /monit

CMD cp -nv /opt/monit.tar.gz /monit
