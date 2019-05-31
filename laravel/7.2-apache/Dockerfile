FROM php:7.2-apache

## Actualizar repositorios
RUN set -xe && apt update
## Instalar paquetes
RUN set -xe \
    && DEBIAN_FRONTEND=noninteractive apt install -y --no-install-recommends wget htop nano zip unzip git git-flow
## Instalar dependencias de extensiones
RUN set -xe \
    && DEBIAN_FRONTEND=noninteractive apt install -y --no-install-recommends \
    ## zip
    zlib1g-dev \
    ## gd
    libpng-dev \
    ## bz2
    libbz2-dev
## Instalar extensiones
RUN docker-php-ext-install mysqli zip gd bz2 bcmath && docker-php-ext-enable mysqli zip gd bz2 bcmath
## Activar mods de apache requeridos
RUN a2enmod rewrite
## Instalar composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
## Crear carpeta de laravel y vincular public al root de apache
RUN set -xe \
    && rm -r /var/www/html \
    && mkdir -p /var/www/laravel/public \
    && chown -R www-data:www-data /var/www \
    && ln -s /var/www/laravel/public /var/www/html \
    && rm -r /var/www/laravel/public
## Declarar volumen para laravel
VOLUME /var/www/laravel
## Heredado de imagen original
EXPOSE 80
## Heredado de imagen original
CMD ["apache2-foreground"]