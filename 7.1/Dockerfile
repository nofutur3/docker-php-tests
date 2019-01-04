FROM nofutur3/php-tests:base-7.1

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
    zlib-dev \
    icu-dev

# install php extensions
RUN docker-php-ext-install \
    bcmath \
    gd \
    iconv \
    mbstring \
    pdo \
    pdo_mysql \
    soap \
    zip \
    intl
