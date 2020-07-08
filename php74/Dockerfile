FROM php:7.4-alpine

MAINTAINER wudner <965391514@qq.com>

ENV PHPREDIS_VERSION 5.1.0
ENV SWOOLE_VERSION 4.5.0

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/bin/

RUN sed -i "s/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g" /etc/apk/repositories \
&& ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
&& echo "Asia/Shanghai" > /etc/timezone \
&& install-php-extensions gd \
    amqp \
    grpc \
    protobuf \
    redis \
    pcntl \
    mcrypt \
    imagick \
    yaml \
    pdo_mysql \
    soap


# Redis extension
RUN wget http://pecl.php.net/get/redis-${PHPREDIS_VERSION}.tgz -O /tmp/redis.tar.tgz \
    && pecl install /tmp/redis.tar.tgz \
    && rm -rf /tmp/redis.tar.tgz \
    && docker-php-ext-enable redis
 # 修改php.ini的文件 extension=redis.so

# Swoole extension
RUN wget https://github.com/swoole/swoole-src/archive/v${SWOOLE_VERSION}.tar.gz -O swoole.tar.gz \
    && mkdir -p swoole \
    && tar -xf swoole.tar.gz -C swoole --strip-components=1 \
    && rm swoole.tar.gz \
    && ( \
        cd swoole \
        && phpize \
        && ./configure  --enable-openssl  --enable-http2 \
        && make -j$(nproc) \
        && make install \
    ) \
    && rm -r swoole \
    && docker-php-ext-enable swoole

# 安装 Composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && composer self-update --clean-backups

#切换镜像
RUN  composer config -g repo.packagist composer https://packagist.laravel-china.org

#设置工作目录
WORKDIR  /var/www





