FROM php:7.4-fpm-alpine

RUN apk add --update \
&& apk add curl \
openssl \
nano

# Common php-ext
RUN apk add libpq zlib openssl-dev curl-dev \
&& docker-php-ext-install pcntl \
&& docker-php-ext-install session \
&& docker-php-ext-install phar \
&& docker-php-ext-install iconv \
&& docker-php-ext-install pdo \
&& docker-php-ext-install curl

# Mcrypt
ARG INSTALL_MCRYPT=false
RUN if [ ${INSTALL_MCRYPT} = true ]; then \
    apk add libmcrypt-dev \
    && docker-php-ext-install mcrypt \
;fi

# Compression
ARG INSTALL_COMPRESSION=false
RUN if [ ${INSTALL_COMPRESSION} = true ]; then \
    
