FROM php:5.6-apache

# Update and upgrade the system
RUN apt-get update && apt-get upgrade -y --no-install-recommends apt-utils

# Install important libraries
RUN apt-get update && apt-get install -y \
    zlib1g-dev\
    libzip-dev \
    build-essential \
    curl \
    libcurl3 \
    libsqlite3-dev \
    git \
 && rm -rf /var/lib/apt/lists/*

# Memcached
RUN apt-get update \
        && buildDeps=" \
                git \
                libmemcached-dev \
                zlib1g-dev \
        " \
        && doNotUninstall=" \
                libmemcached11 \
                libmemcachedutil2 \
        " \
        && apt-get install -y $buildDeps --no-install-recommends \
        && rm -r /var/lib/apt/lists/* \
        \
        && docker-php-source extract \
        && git clone --branch REL2_0 https://github.com/php-memcached-dev/php-memcached /usr/src/php/ext/memcached/ \
        && docker-php-ext-install memcached \
        \
        && docker-php-source delete \
        && apt-mark manual $doNotUninstall \
        && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false $buildDeps

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# PECL Extensions xdebug | imagick
RUN apt-get update && apt-get install -y \
    libmagickwand-dev --no-install-recommends \
    && pecl install xdebug-2.5.5 \
    && pecl install imagick-3.4.3 \
    && docker-php-ext-enable xdebug imagick

# Other PHP7 Extensions
RUN apt-get update && apt-get install -y \
    && docker-php-ext-install bz2 \
    && docker-php-ext-install bcmath \
    && docker-php-ext-install calendar \
    && docker-php-ext-install exif \
    && docker-php-ext-install gettext \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install zip
    
# Enable apache modules
RUN a2enmod rewrite headers
