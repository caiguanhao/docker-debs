FROM buildpack-deps:jessie

WORKDIR /opt/monit-5.12.2

RUN curl -fSs https://mmonit.com/monit/dist/monit-5.12.2.tar.gz | tar --strip-components 1 -xvzf -

ADD simplify.patch /tmp/simplify.patch

RUN patch -p1 -i /tmp/simplify.patch

RUN ./configure --without-pam && make

RUN tar -cv monit monit.1 | gzip -n > monit-5.12.2.tar.gz

VOLUME /monit

CMD cp -nv monit-5.12.2.tar.gz /monit
