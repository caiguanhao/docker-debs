FROM ubuntu:16.04

ADD key /tmp/key

RUN apt-key add /tmp/key && \
echo 'deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main' > /etc/apt/sources.list.d/psql.list

ENV POSTGRESQL_VERSION 9.5

RUN apt-get update && \
    apt-get -d -o Dir::Cache=/opt -o Dir::Cache::archives=postgresql-${POSTGRESQL_VERSION} \
    install --no-install-recommends -y postgresql-${POSTGRESQL_VERSION} postgresql-contrib-${POSTGRESQL_VERSION} && \
    find /opt/postgresql-${POSTGRESQL_VERSION}/* -not -name '*.deb' -delete && \
    cd /opt && tar -cv postgresql-${POSTGRESQL_VERSION} | gzip -n > postgresql-${POSTGRESQL_VERSION}.tar.gz

RUN apt-get -d -o Dir::Cache=/opt -o Dir::Cache::archives=libpq-dev-${POSTGRESQL_VERSION} \
    install --no-install-recommends -y libpq-dev libpq5 && \
    find /opt/libpq-dev-${POSTGRESQL_VERSION}/* -not -name '*.deb' -delete && \
    cd /opt && tar -cv libpq-dev-${POSTGRESQL_VERSION} | gzip -n > libpq-dev-${POSTGRESQL_VERSION}.tar.gz

VOLUME /mnt

CMD cp -v /opt/postgresql-${POSTGRESQL_VERSION}.tar.gz /opt/libpq-dev-${POSTGRESQL_VERSION}.tar.gz /mnt
