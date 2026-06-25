FROM php:8.4-fpm

# Instalar dependencias necesarias para MongoDB, etc.
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    curl \
    libzip-dev \
    libpng-dev \
    libxml2-dev \
    libonig-dev \
    libssl-dev \
    libpq-dev \
    libmongoc-1.0-0 \
    libjemalloc2 \
    && rm -rf /var/lib/apt/lists/*

# Instalar extensiones PHP necesarias
RUN docker-php-ext-install pdo pdo_mysql pdo_pgsql xml ctype zip

# Instalar MongoDB extension
# RUN pecl install mongodb && docker-php-ext-enable mongodb

# Instalar Xdebug
# RUN pecl install xdebug && docker-php-ext-enable xdebug

# Instalar Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Establecer directorio de trabajo
WORKDIR /var/www/html

# Copiar el código Laravel desde /src del repo al contenedor
COPY src/ /var/www/html/

# Copiar .env.**Render**
COPY **Render**/.env.**Render** /var/www/html/.env

# Ejecutar composer install sin dependencias de desarrollo
RUN composer install --optimize-autoloader --no-dev

# Exponer puerto 1000 (o el que uses)
EXPOSE 1000

# Comando para arrancar Laravel con servidor embebido PHP
CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=1000"]