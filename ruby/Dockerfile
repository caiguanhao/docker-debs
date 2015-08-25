FROM ubuntu:14.04

WORKDIR /opt

RUN python3 -c 'from urllib.request import urlopen; from json import loads; \
    print(loads(urlopen("http://ip-api.com/json").read().decode("utf-8" \
    ).strip())["countryCode"])' > /tmp/country

RUN test $(cat /tmp/country) = "CN" && { \
    sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list; \
    } || true

RUN apt-get update && apt-get upgrade -y

RUN apt-get install -y \
      autoconf \
      bison \
      build-essential \
      imagemagick \
      libbz2-dev \
      libcurl4-openssl-dev \
      libevent-dev \
      libffi-dev \
      libglib2.0-dev \
      libgdbm3 \
      libgdbm-dev \
      libjpeg-dev \
      liblzma-dev \
      libmagickcore-dev \
      libmagickwand-dev \
      libmysqlclient-dev \
      libncurses-dev \
      libncurses5-dev \
      libpq-dev \
      libreadline-dev \
      libreadline6-dev \
      libsqlite3-dev \
      libssl-dev \
      libxml2-dev \
      libxslt-dev \
      libyaml-dev \
      zlib1g-dev

RUN apt-get install -y git curl

RUN adduser --disabled-password --gecos '' deploy

RUN su -s /bin/bash deploy -c 'mkdir ~/.ssh && ssh-keyscan -H github.com >> ~/.ssh/known_hosts'

RUN su -s /bin/bash deploy -c 'git clone https://github.com/sstephenson/rbenv.git ~/.rbenv'

RUN su -s /bin/bash deploy -c 'git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build'

ENV RUBY_VERSION 2.2.2

RUN su -s /bin/bash deploy -c 'export PATH="$HOME/.rbenv/bin:$PATH" && \
    eval "$(rbenv init -)" && \
    sed -i "s!http://cache.ruby-lang.org/pub!https://ruby.taobao.org/mirrors!" ~/.rbenv/plugins/ruby-build/share/ruby-build/$RUBY_VERSION && \
    export RUBY_BUILD_SKIP_MIRROR=1 && \
    CONFIGURE_OPTS="--disable-install-doc" rbenv install -f -v $RUBY_VERSION'

RUN su -s /bin/bash deploy -c 'cd ~/.rbenv/versions && tar cfvz ~/ruby-$RUBY_VERSION.tar.gz $RUBY_VERSION'

VOLUME /ruby

CMD cp -nv /home/deploy/ruby-$RUBY_VERSION.tar.gz /ruby
