FROM buildpack-deps:jessie

ENV URL https://github.com/docker/compose/releases/download

ENV COMPOSE_VERSIONS 1.1.0 1.2.0 1.3.0

RUN for COMPOSE_VERSION in $COMPOSE_VERSIONS; do \
    cd /opt && mkdir -p $COMPOSE_VERSION && echo "Downloading $COMPOSE_VERSION..." && \
    curl -fsSL $URL/$COMPOSE_VERSION/docker-compose-Linux-x86_64 -o $COMPOSE_VERSION/docker-compose; \
    done

VOLUME /compose
CMD cp -r /opt/* /compose
