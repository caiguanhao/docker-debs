FROM buildpack-deps:jessie

WORKDIR /opt

ENV RBENV_SHA 3997a39
RUN git clone --no-checkout https://github.com/sstephenson/rbenv.git rbenv-${RBENV_SHA} && \
    cd rbenv-${RBENV_SHA} && git reset --hard ${RBENV_SHA} && \
    cd .. && tar cfvz rbenv-${RBENV_SHA}.tar.gz rbenv-${RBENV_SHA} && \
    mkdir -p rbenv && mv rbenv-${RBENV_SHA}.tar.gz rbenv && rm -rf rbenv-${RBENV_SHA}

ENV RUBY_BUILD_SHA 2882619
RUN git clone --no-checkout https://github.com/sstephenson/ruby-build.git ruby-build-${RUBY_BUILD_SHA} && \
    cd ruby-build-${RUBY_BUILD_SHA} && git reset --hard ${RUBY_BUILD_SHA} && \
    cd .. && tar cfvz ruby-build-${RUBY_BUILD_SHA}.tar.gz ruby-build-${RUBY_BUILD_SHA} && \
    mkdir -p ruby-build && mv ruby-build-${RUBY_BUILD_SHA}.tar.gz ruby-build && rm -rf ruby-build-${RUBY_BUILD_SHA}

ENV ALIASES_SHA e8db255
RUN git clone --no-checkout https://github.com/caiguanhao/aliases.git aliases-${ALIASES_SHA} && \
    cd aliases-${ALIASES_SHA} && git reset --hard ${ALIASES_SHA} && \
    cd .. && tar cfvz aliases-${ALIASES_SHA}.tar.gz aliases-${ALIASES_SHA} && \
    mkdir -p aliases && mv aliases-${ALIASES_SHA}.tar.gz aliases && rm -rf aliases-${ALIASES_SHA}

ENV VIMRC_SHA 85cf4bc
RUN git clone --no-checkout https://github.com/caiguanhao/vimrc.git vimrc-${VIMRC_SHA} && \
    cd vimrc-${VIMRC_SHA} && git reset --hard ${VIMRC_SHA} && ./install.sh && \
    cd .. && tar cfvz vimrc-${VIMRC_SHA}.tar.gz vimrc-${VIMRC_SHA} && \
    mkdir -p vimrc && mv vimrc-${VIMRC_SHA}.tar.gz vimrc && rm -rf vimrc-${VIMRC_SHA}

VOLUME /git
CMD cp -rv /opt/* /git
