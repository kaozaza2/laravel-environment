FROM alpine:3.15

ARG NODE_VERSION=16.16.0
ARG YARN_VERSION=1.22.19

RUN echo "@main http://dl-cdn.alpinelinux.org/alpine/v3.15/main" >> /etc/apk/repositories \
 && echo "@community http://dl-cdn.alpinelinux.org/alpine/v3.15/community" >> /etc/apk/repositories \
 && apk update

RUN apk add --no-cache tar bind-tools curl ca-certificates \
    zip unzip git supervisor sqlite libcap libpng-dev python2 \
 && apk add --no-cache php8-cli php8-dev \
    php8-pgsql php8-sqlite3 php8-gd php8-pear \
    php8-curl php8-imap php8-mbstring php8-xdebug \
    php8-xml php8-zip php8-bcmath php8-soap \
    php8-intl php8-ldap php8-redis \
 && pecl install openswoole \
 && pecl install msgpack \
 && pecl install mysql \
 && pecl install pcov \
 && pecl install readline \
 && pecl install memcached \
 && pecl install igbinary \
 && php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer

RUN curl -fsSLO --compressed "https://unofficial-builds.nodejs.org/download/release/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64-musl.tar.xz" \
 && tar -xJf "node-v$NODE_VERSION-linux-x64-musl.tar.xz" -C /usr/local --strip-components=1 --no-same-owner \
 && ln -s /usr/local/bin/node /usr/local/bin/nodejs \
 && rm -f "node-v$NODE_VERSION-linux-x64-musl.tar.xz"

RUN curl -fsSLO --compressed "https://yarnpkg.com/downloads/$YARN_VERSION/yarn-v$YARN_VERSION.tar.gz" \
 && mkdir -p /opt \
 && tar -xzf yarn-v$YARN_VERSION.tar.gz -C /opt/ \
 && ln -s /opt/yarn-v$YARN_VERSION/bin/yarn /usr/local/bin/yarn \
 && ln -s /opt/yarn-v$YARN_VERSION/bin/yarnpkg /usr/local/bin/yarnpkg \
 && rm -f yarn-v$YARN_VERSION.tar.gz
