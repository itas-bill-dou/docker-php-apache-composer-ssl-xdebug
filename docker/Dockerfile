# PHP Version Support - https://xdebug.org/docs/compat#versions
# Be careful the compatibility issue between Xdebug version and PHP version

ARG PHP_VERSION=8.1
# Use the official PHP image as the base image
FROM php:${PHP_VERSION}-apache

# Define build arguments for credentials
ARG DEMO_USERNAME
ARG DEMO_PASSWORD

# Install system dependencies
RUN apt-get update && apt-get install -y \
    libzip-dev \
    zip \
    unzip \
    git

# Install PHP extensions
RUN docker-php-ext-install zip

# Enable Apache modules
RUN a2enmod headers ssl rewrite \
    && mkdir -p /etc/apache2/ssl

# Install Composer globally
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Without a specified version, it will install the latest version - https://xdebug.org/download/historical
# PHP8
RUN pecl install xdebug && docker-php-ext-enable xdebug

# PHP7
# RUN pecl install xdebug-3.1.6 && docker-php-ext-enable xdebug

# Configure Xdebug
COPY docker/xdebug.ini /usr/local/etc/php/conf.d/

# Copy SSL certificates and Apache configuration
COPY docker/ssl/cert.pem /etc/apache2/ssl/cert.pem
COPY docker/ssl/cert-key.pem /etc/apache2/ssl/cert-key.pem
COPY docker/000-default.conf /etc/apache2/sites-available/000-default.conf

# Set credentials as environment variables during the build
ENV DEMO_USERNAME=${DEMO_USERNAME}
ENV DEMO_PASSWORD=${DEMO_PASSWORD}

# Set the working directory
WORKDIR /var/www/html

# Copy your application code into the container
COPY ../ /var/www/html

# Set ownership to www-data for all files and folders
RUN chown -R www-data:www-data /var/www/html

EXPOSE 443
