FROM nofutur3/php-tests:base-7.4

MAINTAINER Jakub Vyvazil <jakub@vyvazil.cz>

# install libs
RUN apk add --update --no-cache \
        icu-libs \
        libintl \
        libzip \
        aria2 \
        patch

RUN apk add --update --no-cache --virtual .deps \
        freetype-dev \
        libjpeg-turbo-dev \
        libpng-dev \
        gettext-dev \
        gmp-dev \
        icu-dev \
        oniguruma-dev \
        libxml2-dev \
        ldb-dev \
        libzip-dev \
        autoconf \
        g++ \
        make \
        pcre-dev \
        wget


# amqp extension
RUN apk add rabbitmq-c rabbitmq-c-dev autoconf g++ make \
    && pecl install amqp \
    && docker-php-ext-enable amqp

# zip extension
RUN docker-php-ext-configure zip && docker-php-ext-install zip

# install php extensions
RUN docker-php-ext-install \
    bcmath \
    gd \
    iconv \
    mbstring \
    pdo \
    pdo_mysql \
    soap \
    intl \
    sockets

RUN apk del .deps && \
    rm -rf /var/cache/apk/*
