FROM php:8.3-fpm

# System dependencies
RUN apt-get update && apt-get install -y \
    bash \
    curl \
    wget \
    git \
    unzip \
    nano \
    vim \
    cron \
    mariadb-client \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libwebp-dev \
    libxpm-dev \
    libicu-dev \
    libzip-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    && rm -rf /var/lib/apt/lists/*

# PHP extensions required by Drupal 11 / CMS 2
RUN docker-php-ext-configure gd \
    --with-freetype \
    --with-jpeg \
    --with-webp \
    && docker-php-ext-install -j$(nproc) \
        pdo_mysql \
        gd \
        bcmath \
        zip \
        intl \
        opcache

# Enable OPcache (recommended for Drupal)
RUN echo "opcache.enable=1" >> /usr/local/etc/php/conf.d/opcache.ini \
    && echo "opcache.memory_consumption=256" >> /usr/local/etc/php/conf.d/opcache.ini \
    && echo "opcache.max_accelerated_files=20000" >> /usr/local/etc/php/conf.d/opcache.ini \
    && echo "opcache.validate_timestamps=1" >> /usr/local/etc/php/conf.d/opcache.ini

# Install Composer (secure install)
RUN curl -sS https://getcomposer.org/installer -o composer-setup.php \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && rm composer-setup.php

# Increase PHP limits for Drupal
RUN echo "memory_limit=512M" > /usr/local/etc/php/conf.d/memory-limit.ini \
    && echo "upload_max_filesize=100M" >> /usr/local/etc/php/conf.d/memory-limit.ini \
    && echo "post_max_size=100M" >> /usr/local/etc/php/conf.d/memory-limit.ini

# Set working directory
WORKDIR /var/www/html

# Use non-root user
USER www-data

EXPOSE 9000

CMD ["php-fpm"]
