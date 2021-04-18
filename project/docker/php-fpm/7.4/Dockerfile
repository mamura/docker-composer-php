FROM php:7.4-fpm

# Set working directory
WORKDIR /var/www/html

# Install dependecies
RUN apt-get update && apt-get install -y \
    autoconf \
    libc-dev \
    make \
    git \
    pkgconf \
    build-essential \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    libxslt-dev \
    libzip-dev \
    libxml2-dev \
    npm

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install extensions
RUN docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg \
    && docker-php-ext-configure bcmath --enable-bcmath \
    && docker-php-ext-configure intl --enable-intl \
    && docker-php-ext-configure pcntl --enable-pcntl \
    && docker-php-ext-configure mysqli --with-mysqli \
    && docker-php-ext-configure pdo_mysql --with-pdo-mysql \
    && docker-php-ext-configure soap --enable-soap \
    && docker-php-ext-configure opcache --enable-opcache \
    && docker-php-ext-install -j$(nproc) \
        gd \
        bcmath \
        intl \
        pcntl \
        mysqli \
        pdo_mysql \
        soap \
        iconv \
        xsl \
        zip \
        xmlrpc \
        opcache

#Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]