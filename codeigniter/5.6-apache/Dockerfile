FROM php:5.6-apache

## Actualizar repositorios
RUN set -xe && apt-get update
## Instalar paquetes
RUN set -xe \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends wget htop nano zip unzip git git-flow
## Instalar dependencias de extensiones
RUN set -xe \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    ## zip
    zlib1g-dev \
    ## gd
    libpng-dev \
    ## bz2
    libbz2-dev
## Instalar extensiones
RUN docker-php-ext-install mysqli pdo_mysql zip gd bz2 bcmath && docker-php-ext-enable mysqli pdo_mysql zip gd bz2 bcmath
RUN set -xe \
    && pecl install redis-4.3.0 \
    && pecl install xdebug-2.5.5
# Activar mods de apache requeridos
RUN a2enmod rewrite
## Heredado de imagen original
EXPOSE 80
## Heredado de imagen original
CMD ["apache2-foreground"]