FROM php:8-apache

# Update and upgrade the system
RUN apt-get update && apt-get upgrade -y --no-install-recommends apt-utils

# Install useful tools and important libraries
RUN apt-get update && apt-get install -y \
    build-essential \
    ca-certificates \
    curl \
    git \
    libicu-dev \
    libcurl4 \
    libcurl4-openssl-dev \
    libonig-dev \
    libsqlite3-dev \
    libsqlite3-0 \
    libzip-dev \
    nano \
    openssl \
    unzip \
    vim \
    zlib1g-dev\
 && rm -rf /var/lib/apt/lists/*

# Browscap
RUN mkdir -p /usr/local/etc/php/extra/ \
    && curl "http://browscap.org/stream?q=Lite_PHP_BrowsCapINI" -o /usr/local/etc/php/extra/lite_php_browscap.ini

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install xdebug
RUN apt-get update && apt-get install -y \
    --no-install-recommends \
    && pecl install xdebug-3.1.0 \
    && docker-php-ext-enable xdebug

# Install imagick
RUN apt-get update && apt-get install -y \
    libmagickwand-dev --no-install-recommends \
    && pecl install imagick-3.5.1 \
    && docker-php-ext-enable imagick

# Other PHP8 Extensions
RUN apt-get update && apt-get install -y \
    && docker-php-ext-install bcmath \
    && docker-php-ext-install calendar \
    && docker-php-ext-install exif \
    && docker-php-ext-install gd \
    && docker-php-ext-install gettext \
    && docker-php-ext-install intl \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install pdo_sqlite \
    && docker-php-ext-install xml \
    && docker-php-ext-install zip

# Configure MailHog
RUN curl -Lsf 'https://storage.googleapis.com/golang/go1.15.6.linux-amd64.tar.gz' | tar -C '/usr/local' -xvzf -
ENV PATH /usr/local/go/bin:$PATH
RUN go get github.com/mailhog/mhsendmail
RUN cp /root/go/bin/mhsendmail /usr/bin/mhsendmail

# Fully qualified domain name configuration on localhost.
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

# Enable apache modules
RUN a2enmod rewrite headers

# Cleanup
RUN rm -rf /usr/src/*