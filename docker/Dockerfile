#Alpine
FROM alpine:3.14 as common-tools

#PHP-FPM

FROM php:8.2-fpm-alpine as fpm

ARG USER='www-data'
ARG GROUP='www-data'

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/

RUN install-php-extensions @composer-2 \
    bcmath mcrypt pdo_mysql gd intl xdebug opcache \
    && apk --no-cache add bash

USER ${USER}

WORKDIR /var/www/html

CMD php-fpm

EXPOSE 9000


#NGINX

FROM nginx:1.24.0-alpine as nginx

COPY ./docker/nginx/ /etc/nginx/templates

EXPOSE 80
