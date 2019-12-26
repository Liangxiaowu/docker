FROM php:7.3
# Version
ENV PHPREDIS_VERSION 4.0.0
ENV SWOOLE_VERSION 4.4.8
#COPY ./sources.list /etc/apt/sources.list
RUN sed -i 's/deb.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list && sed -i 's/security.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list
# Timezone
RUN /bin/cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo 'Asia/Shanghai' > /etc/timezone

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
        yum \
    && apt-get clean -y \
    && apt-get autoremove -y

# Composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && composer self-update --clean-backups

# 安装 inotify-tools
#RUN wget http://github.com/downloads/rvoicilas/inotify-tools/inotify-tools-3.14.tar.gz -O inotify-tools-3.14.tar.gz \
#    && mkdir -p inotify-tools \
#    && tar -zxvf inotify-tools-3.14.tar.gz -C inotify-tools --strip-components=1 \
#    && rm inotify-tools-3.14.tar.gz \
#    && ( \
#        cd inotify-tools \
#        && ./configure --prefix=/usr/local/inotify \
#        && make \
#        && make install \
#    ) \
#    && rm -rf inotify-tools

# 安装fswatch
#RUN wget https://github.com/emcrisostomo/fswatch/releases/download/1.9.3/fswatch-1.9.3.tar.gz  -O fswatch-1.9.3.tar.gz \
#    && mkdir -p fswatch \
#    && tar -zxvf fswatch-1.9.3.tar.gz -C fswatch --strip-components=1 \
#    && rm fswatch-1.9.3.tar.gz \
#    && ( \
#        cd fswatch \
#        && ./configure \
#        && make \
#        && make install \
#    ) \
#    && rm -rf fswatch


# docker方式安装PDO extension
RUN docker-php-ext-install pdo_mysql

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

# php-inotify 扩展
#RUN wget https://pecl.php.net/get/inotify-2.0.0.tgz -O inotify.tar.gz \
#    && mkdir -p inotify \
#    && tar -xf inotify.tar.gz -C inotify --strip-components=1 \
#    && rm inotify.tar.gz \
#    && ( \
#        cd inotify \
#        && phpize \
#        && ./configure  --enable-openssl  --enable-http2 --enable-inotify \
#        && make -j$(nproc) \
#        && make install \
#    ) \
#    && rm -r inotify \
#    && docker-php-ext-enable inotify


RUN echo "swoole.use_shortname = Off" >> /usr/local/etc/php/conf.d/docker-php-ext-swoole.ini
#切换镜像
RUN  composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

#ENTRYPOINT ["php","/var/www/html/draw_prize/bin/hyperf.php", "start"]

#设置工作目录
WORKDIR  /var/www/html/draw_prize





