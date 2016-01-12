FROM buildpack-deps:jessie

WORKDIR /opt/monit

RUN apt-get update && apt-get install -y bison flex

RUN git clone --branch gm https://github.com/GaiaMagic/monit /opt/monit

RUN sed -i 's#git@bitbucket.org:#https://bitbucket.org/#' .gitmodules

RUN git submodule init && git submodule update

RUN ./bootstrap && ./configure --without-pam && make

RUN tar -cv monit monit.1 | gzip -n > monit.tar.gz

VOLUME /monit

CMD cp -v monit.tar.gz /monit
