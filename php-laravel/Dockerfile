# Use a base image with PHP and the desired version
# FROM php:8.0-apache
FROM systemsdk/docker-apache-php-laravel

# Set the working directory in the container
WORKDIR /var/www/html

# Install system dependencies
RUN apt-get update && apt-get install -y \
    libzip-dev \
    unzip

# Install PHP extensions
RUN docker-php-ext-install pdo_mysql zip

# Enable Apache Rewrite module
RUN a2enmod rewrite

# Set permissions for Laravel
RUN chown -R www-data:www-data /var/www/html
RUN chmod -R 755 /var/www/html/storage

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install Laravel dependencies
RUN composer install --no-interaction --optimize-autoloader --no-dev

RUN composer create-project laravel/laravel myApp
RUN cd myApp
RUN ls
# Generate application key
RUN php artisan key:generate

# Expose the container port
EXPOSE 80
# RUN php artisan serve --host=0.0.0.0 --port=8000
# Start the Apache server
CMD ["apache2-foreground"]