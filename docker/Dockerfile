ARG PHP_VERSION=8.2.3
FROM php:${PHP_VERSION}

## Diretório da aplicação
ARG APP_DIR=/var/www/app/golevel

## Versão da Lib do Redis para PHP
ARG REDIS_LIB_VERSION=5.3.7

### apt-utils é um extensão de recursos do gerenciador de pacotes APT
RUN apt-get update -y && apt-get install -y --no-install-recommends \
    apt-utils \ 
    supervisor

# dependências recomendadas de desenvolvido para ambiente linux
RUN apt-get update && \
    apt-get install -y zlib1g-dev libzip-dev unzip libpng-dev libpq-dev libxml2-dev && \
    docker-php-ext-install mysqli pdo pdo_mysql pdo_pgsql pgsql session xml && \
    pecl install redis-${REDIS_LIB_VERSION} && \
    docker-php-ext-enable redis && \
    docker-php-ext-install zip iconv simplexml pcntl gd fileinfo

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
# Instalação do Node.js e NPM






WORKDIR $APP_DIR
RUN cd $APP_DIR
RUN chown www-data:www-data $APP_DIR


WORKDIR /var/www/app/golevel
RUN rm -rf vendor

RUN apt-get install nginx -y
RUN rm -rf /etc/nginx/sites-enabled/* && rm -rf /etc/nginx/sites-available/*


RUN apt-get clean && rm -rf /var/lib/apt/lists/*
# RUN apt update -y && apt install nano git -y

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisord.conf"]