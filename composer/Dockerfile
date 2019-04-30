FROM composer:latest
ENV PHPREDIS_VERSION 4.2.0
ENV SSH_KEY ""

RUN echo "https://mirrors.aliyun.com/alpine/v3.8/main/" > /etc/apk/repositories \
    && apk add freetype-dev libjpeg-turbo-dev libpng-dev \
    && docker-php-ext-install mbstring bcmath gd calendar fileinfo \
    && mkdir -p /usr/src/php/ext/redis \
    && curl -L -o /tmp/redis.tar.gz https://github.com/phpredis/phpredis/archive/$PHPREDIS_VERSION.tar.gz \
    && tar -zxvf /tmp/redis.tar.gz -C /usr/src/php/ext \
    && mv /usr/src/php/ext/phpredis-* /usr/src/php/ext/phpredis \
    && docker-php-ext-install phpredis \
    && composer global require phpmd/phpmd --no-suggest --no-ansi --no-interaction \
    && ln -s /srv/vendor/bin/phpmd /usr/local/bin/phpmd \
    && mkdir /root/.ssh && \
        echo $SSH_KEY | cut -d "\"" -f 2 > /root/.ssh/id_rsa && \
        chmod 0600 /root/.ssh/id_rsa && \
        eval `ssh-agent -s` && \
        ssh-add /root/.ssh/id_rsa && \
        echo "StrictHostKeyChecking no" >> /etc/ssh/ssh_config