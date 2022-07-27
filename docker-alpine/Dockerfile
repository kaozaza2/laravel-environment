FROM alpine:latest

ARG NODE_VERSION=16.16.0
ARG YARN_VERSION=1.22.19
ARG POSTGRES_VERSION=14

RUN set -xe \
 && apk add --no-cache curl ca-certificates unzip git supervisor sqlite libcap libpng-dev \
    mysql-client postgresql$POSTGRES_VERSION-client pcre \
 && apk add --no-cache gosu --repository="http://dl-cdn.alpinelinux.org/alpine/edge/testing" \
 && apk add --no-cache php81-bcmath php81-common php81-ctype php81-curl \
    php81-dev php81-dom php81-fileinfo php81-gd php81-imap php81-intl php81-sqlite3 \
    php81-mbstring php81-mysqlnd php81-pdo php81-pdo_mysql php81-pecl-igbinary \
    php81-pecl-msgpack php81-pecl-memcached php81-pecl-swoole php81-pecl-xdebug php81-iconv \
    php81-soap php81-tokenizer php81-xml php81-xmlwriter php81-zip php81-simplexml \
    php81-posix php81-ldap php81-openssl php81-phar php81-pcntl php81-pgsql php81-pecl-redis \
    php81-pdo_sqlite php81-pdo_pgsql \
 && if [ ! -f "/usr/bin/php" ]; then ln -s /usr/bin/php81 /usr/bin/php; fi \
 && php --version \
 && php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
 && composer --version \
 && curl -fsSLO --compressed "https://unofficial-builds.nodejs.org/download/release/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64-musl.tar.xz" \
 && tar -xJf "node-v$NODE_VERSION-linux-x64-musl.tar.xz" -C /usr/local --strip-components=1 --no-same-owner \
 && ln -s /usr/local/bin/node /usr/local/bin/nodejs \
 && rm -f "node-v$NODE_VERSION-linux-x64-musl.tar.xz" \
 && node --version \
 && npm --version \
 && curl -fsSLO --compressed "https://yarnpkg.com/downloads/$YARN_VERSION/yarn-v$YARN_VERSION.tar.gz" \
 && mkdir -p /opt \
 && tar -xzf yarn-v$YARN_VERSION.tar.gz -C /opt/ \
 && ln -s /opt/yarn-v$YARN_VERSION/bin/yarn /usr/local/bin/yarn \
 && ln -s /opt/yarn-v$YARN_VERSION/bin/yarnpkg /usr/local/bin/yarnpkg \
 && rm -f yarn-v$YARN_VERSION.tar.gz \
 && yarn --version
