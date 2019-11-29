FROM php:7.3-fpm-alpine

LABEL maintainer "D.Horiyama"

ARG TZ
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer

RUN set -eux \
    && apk add --update-cache --no-cache --virtual=.build-dependencies ${PHPIZE_DEPS} tzdata \
    && cp /usr/share/zoneinfo/${TZ} /etc/localtime \
    && docker-php-ext-install bcmath pdo_mysql \
    && pecl update-channels \
    && pecl install xdebug \
    && apk del .build-dependencies

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
RUN composer global require hirak/prestissimo
