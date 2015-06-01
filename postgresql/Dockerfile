FROM ubuntu:14.04

ADD key /tmp/key

RUN apt-key add /tmp/key && \
    echo 'deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main' > /etc/apt/sources.list.d/psql.list

RUN python3 -c 'from urllib.request import urlopen; from json import loads; \
    print(loads(urlopen("http://ip-api.com/json").read().decode("utf-8" \
    ).strip())["countryCode"])' > /tmp/country

RUN test $(cat /tmp/country) = "CN" && { \
    sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list; \
    } || true

ENV POSTGRESQL_VERSION 9.4

RUN apt-get update && \
    apt-get -d -o Dir::Cache=/opt -o Dir::Cache::archives=postgresql-${POSTGRESQL_VERSION} \
    install -y postgresql-${POSTGRESQL_VERSION} postgresql-contrib-${POSTGRESQL_VERSION} && \
    find /opt/postgresql-${POSTGRESQL_VERSION}/* -not -name '*.deb' -delete && \
    cd /opt && tar -cv postgresql-${POSTGRESQL_VERSION} | gzip -n > postgresql-${POSTGRESQL_VERSION}.tar.gz

RUN apt-get -d -o Dir::Cache=/opt -o Dir::Cache::archives=libpq-dev-${POSTGRESQL_VERSION} \
    install --no-install-recommends -y libpq-dev libpq5 && \
    find /opt/libpq-dev-${POSTGRESQL_VERSION}/* -not -name 'libpq-dev*.deb' -not -name 'libpq5*.deb' -delete && \
    cd /opt && tar -cv libpq-dev-${POSTGRESQL_VERSION} | gzip -n > libpq-dev-${POSTGRESQL_VERSION}.tar.gz

VOLUME /mnt

CMD cp /opt/postgresql-${POSTGRESQL_VERSION}.tar.gz /opt/libpq-dev-${POSTGRESQL_VERSION}.tar.gz /mnt
