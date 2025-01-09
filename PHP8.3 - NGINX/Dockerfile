FROM php:8.3-fpm-alpine3.19

# Install system dependencies
RUN apk add --no-cache \
    bash \
    curl \
    libpng-dev \
    libzip-dev \
    zlib-dev

# Install PHP extensions
RUN docker-php-ext-install gd \
    && docker-php-ext-install zip

# Rename it to php.ini
RUN mv /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini \
    && sed -i "/memory_limit = .*/c\memory_limit =-1" /usr/local/etc/php/php.ini \
    && sed -i "/listen = .*/c\listen = [::]:9000" /usr/local/etc/php-fpm.d/www.conf

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Set working directory
WORKDIR /var/www

EXPOSE 9000
