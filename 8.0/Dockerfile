FROM nofutur3/php-tests:base-8.0

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

# GD extension
RUN apk add --no-cache freetype libpng libjpeg-turbo freetype-dev libpng-dev libjpeg-turbo-dev && \
  docker-php-ext-configure gd \
  && NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) && \
  docker-php-ext-install -j${NPROC} gd && \
  apk del --no-cache freetype-dev libpng-dev libjpeg-turbo-dev

# iconv magic
RUN apk add --no-cache --virtual .iconv-deps \
    g++ \
    gcc \
    make &&\
    mkdir iconv_build

RUN wget https://ftp.gnu.org/pub/gnu/libiconv/libiconv-1.15.tar.gz --output-document=iconv_build/libiconv-1.15.tar.gz &&\
    tar xvzf iconv_build/libiconv-1.15.tar.gz -C iconv_build/


WORKDIR "/iconv_build/libiconv-1.15"
RUN ./configure --prefix=/usr --enable-extra-encodings &&\
    make &&\
    make install
WORKDIR "/"

RUN rm iconv_build -r && apk del .iconv-deps

# zip extension
RUN docker-php-ext-configure zip && docker-php-ext-install zip

# bcmath extension
RUN docker-php-ext-configure bcmath --enable-bcmath && docker-php-ext-install bcmath

# install php extensions
RUN docker-php-ext-install \
    #iconv \
    mbstring \
    pdo \
    pdo_mysql \
    soap \
    intl \
    sockets

RUN php -m

RUN apk del .deps && \
    rm -rf /var/cache/apk/*

#iconv xtra encodings workaround
#RUN apk add --no-cache --repository http://dl-3.alpinelinux.org/alpine/edge/testing gnu-libiconv
ENV LD_PRELOAD /usr/lib/preloadable_libiconv.so
