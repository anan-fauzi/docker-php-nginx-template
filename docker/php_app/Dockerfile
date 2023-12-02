FROM php:8.2-fpm-alpine

RUN echo "UTC" > /etc/timezone
RUN apk add --no-cache zip unzip curl
RUN apk add libstdc++ libzip-dev zip

ENV NODE_VERSION v18.16.0
ENV NODE_PACKAGE_URL https://nodejs.org/dist/${NODE_VERSION}/node-${NODE_VERSION}-linux-x64.tar.xz
WORKDIR /opt
RUN wget $NODE_PACKAGE_URL
RUN mkdir -p /opt/nodejs
RUN tar -xvf *.tar.xz --directory /opt/nodejs --strip-components=1
RUN rm *.tar.xz
RUN ln -s /opt/nodejs/bin/node /usr/local/bin/node
RUN ln -s /opt/nodejs/bin/npm /usr/local/bin/npm

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

