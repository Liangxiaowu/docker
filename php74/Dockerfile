FROM php:7.4-fpm
# Version
ENV PHPREDIS_VERSION 5.1.0
ENV SWOOLE_VERSION 4.5.2


COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/bin/

RUN sed -i 's/deb.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list && sed -i 's/security.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list
# Timezone
RUN /bin/cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo 'Asia/Shanghai' > /etc/timezone

RUN install-php-extensions gd \
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

# Libs
RUN apt-get -y update \
    && apt-get install -y \
        curl \
        vim  \
        wget \
        git \
        zip \
        libz-dev \
        libssl-dev \
        libnghttp2-dev \
        libpcre3-dev \
    && apt-get clean -y \
    && apt-get autoremove -y

# install redis
RUN wget http://pecl.php.net/get/redis-${PHPREDIS_VERSION}.tgz -O /tmp/redis.tar.tgz \
    && pecl install /tmp/redis.tar.tgz \
    && rm -rf /tmp/redis.tar.tgz \
    && docker-php-ext-enable redis

# install swoole https://github.com/swoole/swoole-src/archive/v4.5.2.tar.gz
RUN wget https://github.com/swoole/swoole-src/archive/v${SWOOLE_VERSION}.tar.gz -O swoole.tar.gz \
    && mkdir -p swoole \
    && tar -xf swoole.tar.gz -C swoole --strip-components=1 \
    && rm swoole.tar.gz \
    && ( \
        cd swoole \
        && phpize \
        && ./configure --enable-mysqlnd --enable-openssl --enable-http2 \
        && make -j$(nproc) && make install \
    ) \
    && rm -r swoole \
    && docker-php-ext-enable swoole

# install composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && composer self-update --clean-backups

#设置工作目录
WORKDIR  /var/www
