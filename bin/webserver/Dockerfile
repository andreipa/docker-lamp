FROM php:7.3-apache

# Update and upgrade the system
RUN apt-get update && apt-get upgrade -y --no-install-recommends apt-utils

# Install important libraries
RUN apt-get update && apt-get install -y \
    build-essential \
    curl \
    git \
    libcurl3 \
    libsqlite3-dev \
    libzip-dev \
    zlib1g-dev\
 && rm -rf /var/lib/apt/lists/*

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# PECL Extensions xdebug | imagick
RUN apt-get update && apt-get install -y \
    libmagickwand-dev --no-install-recommends \
    && pecl install xdebug-2.7.0RC1 \
    && pecl install imagick-3.4.3 \
    && docker-php-ext-enable xdebug imagick

# Other PHP7 Extensions
RUN apt-get update && apt-get install -y \
    && docker-php-ext-install bcmath \
    && docker-php-ext-install calendar \
    && docker-php-ext-install exif \
    && docker-php-ext-install gettext \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install zip
    
# Enable apache modules
RUN a2enmod rewrite headers
