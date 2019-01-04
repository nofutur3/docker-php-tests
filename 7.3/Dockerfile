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

# hacks
RUN apk add gnu-libiconv --update-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing/ --allow-untrusted
#RUN ln -s /lib/libz.so /usr/lib/ && ln -s /lib/libz.a /usr/lib

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
