FROM ubuntu:16.04

WORKDIR /opt

RUN echo "deb-src http://nginx.org/packages/mainline/ubuntu xenial nginx" > \
    /etc/apt/sources.list.d/nginx.list && \
    apt-key adv --fetch-keys http://nginx.org/keys/nginx_signing.key && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y dpkg-dev debhelper libssl-dev libpcre3-dev zlib1g-dev quilt lsb-release

RUN apt-get source nginx

RUN curl -Ls https://github.com/vozlt/nginx-module-vts/archive/v0.1.11.tar.gz | tar xfvz -

ADD source.patch /opt/source.patch

RUN cd nginx-* && patch -p1 -i /opt/source.patch && \
    echo 'debian/build-nginx/objs/ngx_http_vhost_traffic_status_module.so usr/lib/nginx/modules' >> debian/nginx.install

RUN cd nginx-* && dpkg-buildpackage -b

VOLUME /nginx

CMD cp -v nginx_*_amd64.deb /nginx
