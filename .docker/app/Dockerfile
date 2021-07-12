FROM php:zts-buster

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"

RUN php composer-setup.php --install-dir=/usr/local/bin --filename=composer

RUN pecl install xdebug

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y git

RUN apt-get install -y \
        libzip-dev \
        zip wget \
  && docker-php-ext-install zip

RUN wget https://get.symfony.com/cli/installer -O - | bash

RUN mv /root/.symfony/bin/symfony /usr/local/bin/symfony

RUN symfony server:ca:install

RUN symfony proxy:start

RUN symfony proxy:domain:attach app

WORKDIR /var/www/html
