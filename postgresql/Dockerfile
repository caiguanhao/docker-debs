FROM ubuntu:14.04

ENV POSTGRESQL_VERSION 9.4

RUN echo 'deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main' > /etc/apt/sources.list.d/psql.list

ADD key /tmp/key

RUN apt-key add /tmp/key

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get -d -o Dir::Cache=/opt -o Dir::Cache::archives=postgresql-${POSTGRESQL_VERSION} \
    install -y postgresql-${POSTGRESQL_VERSION} postgresql-contrib-${POSTGRESQL_VERSION} && \
    find /opt/postgresql-${POSTGRESQL_VERSION}/* -not -name '*.deb' -delete && \
    cd /opt && tar -cv postgresql-${POSTGRESQL_VERSION} | gzip -n > postgresql-${POSTGRESQL_VERSION}.tar.gz

VOLUME /mnt

CMD cp /opt/postgresql-${POSTGRESQL_VERSION}.tar.gz /mnt
