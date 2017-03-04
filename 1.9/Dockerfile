FROM php:5-apache

ARG MAGENTO_TAR_GZ

# Install PHP extensions needed by Magento
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        libxml2-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install -j$(nproc) soap \
    && docker-php-ext-install -j$(nproc) pdo_mysql

# Docker extracts the content for us, so /var/www/magento directory is created.
ADD ${MAGENTO_TAR_GZ} /var/www/
RUN rmdir /var/www/html && mv /var/www/magento /var/www/html && chown -R www-data:www-data /var/www/html
