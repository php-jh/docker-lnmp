FROM php:5.6-fpm

# 添加源：方式一
RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak
ADD sources.list /etc/apt/sources.list
# 添加源：方式二
#RUN sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list
#RUN sed -i 's/security.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list

# 更新
RUN rm -rf /var/lib/apt/lists/* && apt-get clean -y && apt-get update && pecl channel-update pecl.php.net

# 安装
RUN apt-get update && apt-get install -y \
        libmemcached-dev \
        libxml2-dev \
        zlib1g-dev \
        vim \
        xvfb \
        libxrender1 \
        libfontconfig1 \
        libssl-dev \
        ffmpeg \
        zip \
        unzip

# gd
RUN apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

# opcache
RUN docker-php-ext-install opcache
COPY opcache.ini /usr/local/etc/php/conf.d/opcache.ini

# pcntl mysqli pdo_mysql soap zip sockets mbstring exif bcmath
RUN docker-php-ext-install pcntl mysqli pdo_mysql soap zip sockets mbstring exif bcmath

# redis https://pecl.php.net/package/redis
COPY redis-4.2.0.tgz /home
RUN pecl install /home/redis-4.2.0.tgz && \
    docker-php-ext-enable redis && \
    rm /home/redis-4.2.0.tgz

# mongodb https://pecl.php.net/package/mongodb
COPY mongodb-1.5.3.tgz /home
RUN pecl install /home/mongodb-1.5.3.tgz && \
    docker-php-ext-enable mongodb && \
    rm /home/mongodb-1.5.3.tgz

# memcached https://pecl.php.net/package/memcached
#COPY memcached-3.1.3.tgz /home
#RUN pecl install /home/memcached-3.1.3.tgz && \
#    docker-php-ext-enable memcached && \
#    rm /home/memcached-3.1.3.tgz

# swoole https://pecl.php.net/package/swoole
#COPY swoole-4.3.5.tgz /home
#RUN pecl install /home/swoole-4.3.5.tgz && \
#    docker-php-ext-enable swoole && \
#    rm /home/swoole-4.3.5.tgz

# yaf http://pecl.php.net/package/yaf
#COPY yaf-3.0.8.tgz /home
#RUN pecl install /home/yaf-3.0.8.tgz && \
#    docker-php-ext-enable yaf && \
#    rm /home/yaf-3.0.8.tgz

# php 配置文件
ADD php.ini /usr/local/etc/php/php.ini

# Git
#RUN apt-get install -y git

# Composer
ADD composer.phar /usr/local/bin/composer
RUN composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

# 字体
#ADD fonts/msyh.ttc /usr/share/fonts
#ADD fonts/msyhl.ttc /usr/share/fonts
#ADD fonts/msyhbd.ttc /usr/share/fonts

# 安装 wkhtmltopdf
ADD wkhtmltopdf/wkhtmltopdf /usr/bin/wkhtmltopdf
RUN chmod 755 /usr/bin/wkhtmltopdf
RUN apt-get clean
# 添加 wkhtmltopdf 启动脚本
ADD wkhtmltopdf/startup /usr/bin/startup
RUN chmod 755 /usr/bin/startup

USER root

# 清理
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    rm /var/log/lastlog /var/log/faillog

RUN usermod -u 1000 www-data

WORKDIR /var/www

CMD ["php-fpm"]

EXPOSE 9000