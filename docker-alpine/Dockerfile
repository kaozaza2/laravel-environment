FROM alpine:3.16

ARG NODE_VERSION=16.16.0
ARG YARN_VERSION=1.22.19
ARG POSTGRES_VERSION=14

RUN set -xe \
 && apk add --no-cache curl ca-certificates zip unzip git supervisor sqlite libcap libpng-dev \
 && apk add --no-cache php81-common php81-dev php81-pgsql php81-phar \
    php81-sqlite3 php81-gd php81-curl php81-imap php81-mysqli \
    php81-mbstring php81-xml php81-zip php81-bcmath php81-soap \
    php81-intl php81-ldap php81-pecl-msgpack php81-pecl-igbinary \
    php81-pecl-redis php81-pecl-swoole php81-pecl-memcached \
    php81-pecl-xdebug php81-tokenizer php81-pdo php81-pdo_mysql \
 && ln -s /usr/bin/php81 /usr/bin/php \
 && php --version \
 && php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
 && composer --version

RUN curl -fsSLO --compressed "https://unofficial-builds.nodejs.org/download/release/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64-musl.tar.xz" \
 && tar -xJf "node-v$NODE_VERSION-linux-x64-musl.tar.xz" -C /usr/local --strip-components=1 --no-same-owner \
 && ln -s /usr/local/bin/node /usr/local/bin/nodejs \
 && rm -f "node-v$NODE_VERSION-linux-x64-musl.tar.xz" \
 && node --version \
 && npm --version

RUN curl -fsSLO --compressed "https://yarnpkg.com/downloads/$YARN_VERSION/yarn-v$YARN_VERSION.tar.gz" \
 && mkdir -p /opt \
 && tar -xzf yarn-v$YARN_VERSION.tar.gz -C /opt/ \
 && ln -s /opt/yarn-v$YARN_VERSION/bin/yarn /usr/local/bin/yarn \
 && ln -s /opt/yarn-v$YARN_VERSION/bin/yarnpkg /usr/local/bin/yarnpkg \
 && rm -f yarn-v$YARN_VERSION.tar.gz \
 && yarn --version

RUN set -xe \
 && apk add --no-cache postgresql$POSTGRES_VERSION-client
