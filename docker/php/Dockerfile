FROM php:8.2-fpm-alpine

RUN echo "UTC" > /etc/timezone
RUN apk add --no-cache zip unzip curl
RUN apk add libstdc++ libzip-dev zip

RUN apk --update add nodejs
RUN apk --update add npm

WORKDIR /var/www/public-html/app

RUN apk add libpng \ 
             libpng-dev \ 
             libjpeg-turbo-dev \ 
             libwebp-dev zlib-dev \ 
             libxpm-dev && docker-php-ext-install gd \ 
             zip pdo pdo_mysql

RUN curl -sS https://getcomposer.org/installer -o composer-setup.php
RUN php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN rm -rf composer-setup.php

EXPOSE 8000

CMD ["php-fpm"]

