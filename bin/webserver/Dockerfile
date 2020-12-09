FROM php:7.4-apache

# Update and upgrade the system
RUN apt-get update && apt-get upgrade -y --no-install-recommends apt-utils

# Install important libraries
RUN apt-get update && apt-get install -y \
    build-essential \
    ca-certificates \
    curl \
    git \
    libcurl4 \
    libonig-dev \
    libsqlite3-dev \
    libzip-dev \
    nano \
    unzip \
    vim \
    zlib1g-dev\
 && rm -rf /var/lib/apt/lists/*

# Browscap
RUN mkdir -p /usr/local/etc/php/extra/ \
    && curl "http://browscap.org/stream?q=Lite_PHP_BrowsCapINI" -o /usr/local/etc/php/extra/lite_php_browscap.ini

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Configure MailHog
RUN curl -Lsf 'https://storage.googleapis.com/golang/go1.15.6.linux-amd64.tar.gz' | tar -C '/usr/local' -xvzf -
ENV PATH /usr/local/go/bin:$PATH
RUN go get github.com/mailhog/mhsendmail
RUN cp /root/go/bin/mhsendmail /usr/bin/mhsendmail

# Fully qualified domain name configuration on localhost.
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

# PECL Extensions xdebug | imagick
RUN apt-get update && apt-get install -y \
    libmagickwand-dev --no-install-recommends \
    && pecl install xdebug-3.0.1 \
    && pecl install imagick-3.4.4 \
    && docker-php-ext-enable xdebug imagick

# Other PHP7 Extensions
RUN apt-get update && apt-get install -y \
    && docker-php-ext-install bcmath \
    && docker-php-ext-install calendar \
    && docker-php-ext-install exif \
    && docker-php-ext-install gettext \
    && docker-php-ext-install intl \
    && docker-php-ext-install json \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install xml \
    && docker-php-ext-install zip
    
# Enable apache modules
RUN a2enmod rewrite headers