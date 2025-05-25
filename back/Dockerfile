FROM php:8.2-fpm-alpine

# Installer les dépendances nécessaires pour Laravel
RUN apk add --no-cache \
    curl \
    zip \
    unzip \
    git \
    libpng-dev \
    libzip-dev \
    oniguruma-dev \
    libmemcached-dev \
    openssl-dev \
    zlib-dev \
    autoconf \
    gcc \
    g++ \
    make

# Installer les extensions PHP nécessaires pour Laravel
RUN docker-php-ext-install pdo pdo_mysql mbstring exif pcntl bcmath gd zip

# Installer Redis extension
RUN pecl install redis && docker-php-ext-enable redis

# Installer Memcached extension
RUN pecl install memcached && docker-php-ext-enable memcached

# Installer Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

WORKDIR /var/www/html

# Copier tout le code source
COPY . .

# Installer les dépendances PHP sans les scripts automatiques
RUN composer install --no-dev --no-scripts

# Donner la permission à www-data
RUN chown -R www-data:www-data /var/www/html

# Définir l'utilisateur par défaut
USER www-data

# Exposer le port 9000 pour PHP-FPM
EXPOSE 9000

# Démarrer PHP-FPM
CMD ["php-fpm"]
