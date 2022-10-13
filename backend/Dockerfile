# PHP server container
FROM php:7.4-apache AS php-server

RUN a2enmod rewrite
RUN service apache2 restart

RUN apt update && apt install -y libicu-dev && rm -rf /var/lib/apt/lists/*
RUN docker-php-ext-install pdo pdo_mysql intl

# PHP server container debug mode
FROM php-server AS php-server-debug

RUN pecl install xdebug
COPY server/docker/90-xdebug.ini "${PHP_INI_DIR}/conf.d"



# PHP container to run scripts
FROM php:7.4 AS php-script

RUN apt update && apt install -y libicu-dev && rm -rf /var/lib/apt/lists/*
RUN docker-php-ext-install pdo pdo_mysql intl

# PHP container to run scripts debug mode
FROM php-script AS php-script-debug

RUN pecl install xdebug
COPY server/docker/90-xdebug.ini "${PHP_INI_DIR}/conf.d"