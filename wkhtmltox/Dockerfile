FROM ubuntu:14.04

WORKDIR /wkhtmltox

RUN python3 -c 'from urllib.request import urlopen; from json import loads; \
    print(loads(urlopen("http://ip-api.com/json").read().decode("utf-8" \
    ).strip())["countryCode"])' > /tmp/country

RUN test $(cat /tmp/country) = "CN" && { \
    sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list; \
    } || true

RUN apt-get update && apt-get upgrade -y

ENV WKHTMLTOX_VERSION 0.12.2.1

RUN python3 -c "from urllib.request import urlretrieve; \
    urlretrieve('http://downloads.sourceforge.net/wkhtmltopdf/wkhtmltox-${WKHTMLTOX_VERSION}_linux-trusty-amd64.deb', \
    'wkhtmltox-${WKHTMLTOX_VERSION}_linux-trusty-amd64.deb')"

RUN dpkg-deb --showformat '${Depends}\n' -W wkhtmltox-${WKHTMLTOX_VERSION}_linux-trusty-amd64.deb | \
    sed -e 's/([^)]*)//g' -e 's/\s*,\s*/ /g' | \
    xargs apt-get -d -o Dir::Cache=/opt -o Dir::Cache::archives=wkhtmltox-${WKHTMLTOX_VERSION} \
    install -y ttf-wqy-microhei ttf-dejavu ttf-dejavu-extra

RUN find /opt/wkhtmltox-${WKHTMLTOX_VERSION}/* -not -name '*.deb' -delete && \
    mv wkhtmltox-${WKHTMLTOX_VERSION}_linux-trusty-amd64.deb /opt/wkhtmltox-${WKHTMLTOX_VERSION} && \
    cd /opt && tar -cv wkhtmltox-${WKHTMLTOX_VERSION} | gzip -n > wkhtmltox-${WKHTMLTOX_VERSION}.tar.gz

CMD cp -nv /opt/wkhtmltox-${WKHTMLTOX_VERSION}.tar.gz /wkhtmltox
