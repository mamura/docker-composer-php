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
    apk add zip libzip-dev \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip \
;fi

# GD
ARG INSTALL_GD=false
RUN if [ ${INSTALL_GD} = true ]; then \
    apk add freetype libpng libjpeg-turbo freetype-dev libpng-dev libjpeg-turbo-dev \
    && docker-php-ext-configure gd \
    --with-freetype \
    --with-jpeg \
    && NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) \
    && docker-php-ext-install -j${NPROC} gd \
    && apk del --no-cache freetype-dev libpng-dev libjpeg-turbo-dev
;fi

# Mbstring
ARG INSTALL_MBSTRING=false
RUN if [ ${INSTALL_MBSTRING} = true ]; then \
    docker-php-ext-install mbstring \
;fi    

# PDO Mysql
ARG INSTALL_PDO_MYSQL=false
RUN if [ ${INSTALL_MYSQL} = true ]; then \
    apk add mariadb-client \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mysqli
;fi

# PDO PostgreSql
ARG INSTALL_PDO_PGSQL=false
RUN if [ ${INSTALL_PDO_PGSQL} = true ]; then \
    docker-php-ext-install pdo_pgsql \
;fi

# bcmath
ARG INSTALL_BCMATH=false
RUN if [ ${INSTALL_BCMATH} = true ]; then \
    docker-php-ext-install bcmath \
;fi

# Opcache
ARG INSTALL_OPCACHE=false
RUN if [ ${INSTALL_OPCACHE} = true ]; then \
    docker-php-ext-install opcache \
;fi
COPY ./opcache.ini /usr/local/etc/php/conf.d/opcache.ini

# Xdebug
ARG INSTALL_XDEBUG=false
RUN if [ ${INSTALL_XDEBUG} = true ]; then \
    pecl install xdebug \
    docker-php-ext-enable xbedug \
;fi
COPY ./xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

# Composer
ARG INSTALL_COMPOSER
RUN if [ ${INSTALL_COMPOSER} = true ]; then \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
;fi

# Tokenizer
ARG INSTALL_TOKENIZER=false
RUN if [ ${INSTALL_TOKENIZER} = true ]; then \
    docker-php-ext-install tokenizer \
;fi

# json, xml, dim, xmlrpc, xsl
ARG INSTALL_JSON=false
RUN if [ ${INSTALL_JSON} = true ]; then \
    apk add libxml2-dev libxslt-dev \
    && docker-php-ext-install json \
    xml \
    dom \
    xmlrpc \
    xsl
;fi

# intl
ARG INSTALL_INTL=false
RUN if [ ${INSTALL_JSON} = true ]; then \
    apk add zlib-dev icu-dev g++ \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl
;fi

# node
ARG INSTALL_NODE=false
RUN if [ ${INSTALL_NODE} = true ]; then \
    apk add nodejs npm \
;fi

# Permissions
RUN chown -R root:www-data /var/www/html
RUN chmod u+rwx,g+rx,o+rx /var/www/html
RUN find /var/www/html -type d -exec chmod u+rwx,g+rx,o+rx {} +
RUN find /var/www/html -type f -exec chmod u+rw,g+rw,o+r {} +

RUN cp /usr/local/etc/php/php.ini-production /usr/local/etc/php/php.ini

CMD ["php-fpm"]

EXPOSE 9000