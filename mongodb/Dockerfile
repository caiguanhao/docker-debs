FROM ubuntu:20.04

RUN apt-get update && apt-get upgrade -y && apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

RUN curl -fsSL https://www.mongodb.org/static/pgp/server-4.4.asc | apt-key add -

RUN echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/4.4 multiverse" >> /etc/apt/sources.list.d/mongodb-org-4.4.list

ENV MONGODB_VERESION 4.4.0

RUN apt-get update && apt-get --no-install-recommends -d \
       -o Dir::Cache=/opt \
       -o Dir::Cache::archives=mongodb-$MONGODB_VERESION \
       install -y mongodb-org=$MONGODB_VERESION

RUN find /opt/mongodb-$MONGODB_VERESION/* -not -name '*.deb' -delete && \
    cd /opt && tar -cv mongodb-$MONGODB_VERESION | gzip -n > mongodb-$MONGODB_VERESION.tar.gz

VOLUME /mongodb

CMD cp -nv /opt/mongodb-$MONGODB_VERESION.tar.gz /mongodb
