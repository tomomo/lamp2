FROM node:16-alpine as node
FROM php:8.0-fpm-alpine

RUN \
  apk add --no-cache --virtual .build-deps autoconf build-base postgresql-dev && \
  apk add --no-cache \
    shadow \
    bzip2-dev \
    gettext-dev \
    postgresql-libs \
    icu-dev \
    imagemagick-dev libpng-dev libjpeg-turbo-dev \
    libzip-dev \
  && \
  pecl install imagick redis && \
  docker-php-ext-enable imagick redis \
  && \
  NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) && \
  docker-php-ext-install -j${NPROC} \
    bcmath \
    bz2 \
    calendar \
    exif \
    gd \
    gettext \
    intl \
    mysqli pdo_mysql \
    pgsql pdo_pgsql \
    sockets \
    zip \
  && \
  apk del --purge .build-deps

COPY --from=composer /usr/bin/composer /usr/bin/composer
COPY --from=node /usr/local/bin/node /usr/local/bin/
COPY --from=node /usr/local/lib/node_modules/ /usr/local/lib/node_modules/
COPY --from=node /opt/yarn* /opt/yarn

ARG UID=1000
RUN usermod -u ${UID} www-data && \
  { \
    echo ''; \
    echo 'security.limit_extensions = .php .html'; \
  } >> /usr/local/etc/php-fpm.d/www.conf && \
  ln -s /usr/local/bin/node /usr/local/bin/nodejs && \
  ln -s /usr/local/lib/node_modules/npm/bin/npm-cli.js /usr/local/bin/npm && \
  ln -s /usr/local/lib/node_modules/npm/bin/npm-cli.js /usr/local/bin/npx && \
  ln -s /opt/yarn/bin/yarn /usr/local/bin/yarn && \
  ln -s /opt/yarn/bin/yarnpkg /usr/local/bin/yarnpkg
