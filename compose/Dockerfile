FROM buildpack-deps:jessie

ENV URL https://github.com/docker/compose/releases/download

ENV COMPOSE_VERSIONS 1.5.2

RUN for COMPOSE_VERSION in $COMPOSE_VERSIONS; do \
    cd /opt && mkdir -p $COMPOSE_VERSION && cd $COMPOSE_VERSION && \
    rm -f _docker-compose && test ! -f docker-compose && \
    echo "Downloading $COMPOSE_VERSION..." && \
    curl -fsSL $URL/$COMPOSE_VERSION/docker-compose-Linux-x86_64 -o _docker-compose && \
    mv _docker-compose docker-compose; \
    done

VOLUME /compose
CMD cp -rnv /opt/* /compose
