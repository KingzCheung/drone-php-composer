FROM composer:latest
ENV PHPREDIS_VERSION 4.2.0


RUN echo "https://mirrors.aliyun.com/alpine/v3.8/main/" > /etc/apk/repositories \
    && apk add freetype-dev libjpeg-turbo-dev libpng-dev \
    && docker-php-ext-install mbstring bcmath gd calendar fileinfo \
    && mkdir -p /usr/src/php/ext/redis \
    && curl -L -o /tmp/redis.tar.gz https://github.com/phpredis/phpredis/archive/$PHPREDIS_VERSION.tar.gz \
    && tar -zxvf /tmp/redis.tar.gz -C /usr/src/php/ext \
    && mv /usr/src/php/ext/phpredis-* /usr/src/php/ext/phpredis \
    && docker-php-ext-install phpredis \
    && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/ \
    && composer global require phpmd/phpmd --no-suggest --no-ansi --no-interaction \
    && ln -s /srv/vendor/bin/phpmd /usr/local/bin/phpmd \
    && mkdir -p /root/.ssh
