FROM nofutur3/php-tests:base-7.3

MAINTAINER Jakub Vyvazil <jakub@vyvazil.cz>

# install libs
RUN apk add --update \
    freetype \
    freetype-dev \
    libgcrypt-dev \
    libjpeg-turbo \
    libjpeg-turbo-dev \
    libpng \
    libpng-dev \
    libxml2-dev \
    #libzip \
    zlib-dev \
    icu-dev

# prepare compilator and dir for iconv build
RUN apk add --no-cache --virtual .build-deps \
    g++ \
    gcc \
    make &&\
    mkdir iconv_build

# download and extract iconv source
RUN wget https://ftp.gnu.org/pub/gnu/libiconv/libiconv-1.15.tar.gz --output-document=iconv_build/libiconv-1.15.tar.gz &&\
    tar xvzf iconv_build/libiconv-1.15.tar.gz -C iconv_build/

# build iconv lib
WORKDIR "/iconv_build/libiconv-1.15"
RUN ./configure --prefix=/usr --enable-extra-encodings &&\
    make &&\
    make install
WORKDIR "/"

# clear image after iconv build
RUN rm iconv_build -r && apk del .build-deps

# amqp extension
RUN apk add rabbitmq-c rabbitmq-c-dev autoconf g++ make \
    && pecl install amqp \
    && docker-php-ext-enable amqp

# install php extensions
RUN docker-php-ext-install \
    bcmath \
    gd \
    iconv \
    mbstring \
    pdo \
    pdo_mysql \
    soap \
    #zip
    intl

# Fix for iconv: https://github.com/docker-library/php/issues/240
ENV LD_PRELOAD /usr/lib/preloadable_libiconv.so php
