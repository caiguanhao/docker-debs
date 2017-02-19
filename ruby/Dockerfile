FROM ubuntu:16.04

WORKDIR /opt

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

RUN su -s /bin/bash deploy -c 'export PATH="$HOME/.rbenv/bin:$PATH" && \
    eval "$(rbenv init -)" && \
    CONFIGURE_OPTS="--disable-install-doc" rbenv install -f -v 2.3.3 && \
    cd ~/.rbenv/versions && tar cfvz ~/ruby-2.3.3.tar.gz 2.3.3'

RUN su -s /bin/bash deploy -c 'export PATH="$HOME/.rbenv/bin:$PATH" && \
    eval "$(rbenv init -)" && \
    CONFIGURE_OPTS="--disable-install-doc" rbenv install -f -v 2.4.0 && \
    cd ~/.rbenv/versions && tar cfvz ~/ruby-2.4.0.tar.gz 2.4.0'

VOLUME /ruby

CMD cp -v /home/deploy/ruby-*.tar.gz /ruby
