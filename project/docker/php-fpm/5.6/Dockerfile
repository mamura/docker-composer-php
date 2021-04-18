FROM php:5.6

# Set work directory
WORKDIR /var/www/html

# Install dependecies
RUN apt-get update && apt-get install -y \
    build-essential \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    libmcrypt-dev \
    locales \
    zip \
    jpegoptim optipng pngquant gifsicle \
    nano \
    unzip \
    git \
    curl

    # Clean cache
    RUN apt-get clean && rm -rf /var/lib/apt/lists/*

    # Install extensions
    RUN docker-php-ext-install -j$(nproc) mysqli pdo pdo_mysql mbstring zip exif pcntl iconv mcrypt
    RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
    RUN docker-php-ext-install -j$(nproc) gd

    # Composer
    RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

    # Expose port 9000 and start php-fpm server
    EXPOSE 9000
    CMD ["php-fpm"]