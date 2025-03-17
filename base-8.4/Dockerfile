FROM php:8.4-alpine

LABEL org.opencontainers.image.authors="jakub@vyvazil.cz"

# update libs
RUN apk update && apk upgrade

# install libs
RUN apk add --update --no-cache \
    git \
    libstdc++ \
    openssh-client \
    gnupg

# --> install phive
RUN wget -O phive.phar "https://phar.io/releases/phive.phar" \
    && wget -O phive.phar.asc "https://phar.io/releases/phive.phar.asc" \
    && gpg --keyserver hkps://keys.openpgp.org --recv-keys 0x6AF725270AB81E04D79442549D8A98B29B2D5D79 \
    && gpg --verify phive.phar.asc phive.phar \
    && rm phive.phar.asc \
    && chmod +x phive.phar \
    && mv phive.phar /usr/local/bin/phive

# --> install composer
COPY --from=composer:2.8 /usr/bin/composer /usr/bin/composer

# --> get node & npm from node image
COPY --from=node:lts-alpine /usr/local/bin /usr/local/bin
COPY --from=node:lts-alpine /usr/local/lib/node_modules /usr/local/lib/node_modules
