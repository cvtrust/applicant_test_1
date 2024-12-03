ARG NODE_VERSION=18.16.0

FROM node:${NODE_VERSION}-alpine AS node
FROM --platform=linux/amd64 php:8.3-fpm-alpine

RUN apk --update add \
    bash \
    wget \
    curl \
    build-base \
    libmcrypt-dev \
    libxml2-dev \
    pcre-dev \
    zlib-dev \
    autoconf \
    oniguruma-dev \
    openssl \
    openssl-dev \
    freetype-dev \
    libjpeg-turbo-dev \
    jpeg-dev \
    libpng-dev \
    imagemagick-dev \
    imagemagick \
    postgresql-dev \
    libzip-dev \
    gettext-dev \
    libxslt-dev \
    libgcrypt-dev \
    linux-headers && \
    rm /var/cache/apk/*

RUN pecl channel-update pecl.php.net && \
    pecl install mcrypt redis-6.0.1 && \
    rm -rf /tmp/pear

RUN docker-php-ext-install \
    mysqli \
    mbstring \
    pdo \
    pdo_pgsql \
    xml \
    pcntl \
    bcmath \
    zip \
    intl \
    gettext \
    soap \
    xsl

RUN apk --update add \
    php-dom \
    php-fileinfo \
    php-session \
    php-simplexml \
    php-tokenizer \
    php-xml \
    php-xmlwriter  && \
    rm /var/cache/apk/*

RUN apk --update add composer && \
    composer require laravel/vapor-cli --update-with-dependencies

RUN apk --update add \
    php-dom \
    php-fileinfo \
    php-session \
    php-simplexml \
    php-tokenizer \
    php-xml \
    php-xmlwriter  && \
    rm /var/cache/apk/*

COPY --from=node /usr/lib /usr/lib
COPY --from=node /usr/local/lib /usr/local/lib
COPY --from=node /usr/local/include /usr/local/include
COPY --from=node /usr/local/bin /usr/local/bin

WORKDIR /app

