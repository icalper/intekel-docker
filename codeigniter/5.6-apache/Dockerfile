FROM php:5.6-apache-stretch
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
    libbz2-dev \
    ## soap, xml
    libxml2 libxml2-dev
## Instalar extensiones
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install zip
RUN docker-php-ext-install gd
RUN docker-php-ext-install bz2
RUN docker-php-ext-install bcmath
RUN docker-php-ext-install xml
RUN docker-php-ext-install soap
RUN set -xe \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends libxslt1-dev libxslt1.1\
    && docker-php-ext-install xsl
RUN set -xe \
    && pecl install redis-4.3.0 \
    && pecl install xdebug-2.5.5
# Activar mods de apache requeridos
RUN a2enmod rewrite
## Zona horaria
ENV TZ=America/Mexico_City
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
## Heredado de imagen original
EXPOSE 80
## Heredado de imagen original
CMD ["apache2-foreground"]