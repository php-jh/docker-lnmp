FROM php:7.4-fpm

# 添加源：方式一
#RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak
#ADD sources.list /etc/apt/sources.list

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd

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

# memcached https://pecl.php.net/package/memcached
#COPY memcached-3.1.3.tgz /home
#RUN pecl install /home/memcached-3.1.3.tgz && \
#    docker-php-ext-enable memcached && \
#    rm /home/memcached-3.1.3.tgz


WORKDIR /var/www

CMD ["php-fpm"]

EXPOSE 9000

RUN pecl install redis \
    && pecl install memcached \
    && pecl install swoole \
    && pecl install mongodb \
    && pecl install yaf \
    && docker-php-ext-enable redis swoole memcached mongodb yaf


#composer安装
ADD composer.phar /usr/local/bin/composer
RUN composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

# 安装 wkhtmltopdf
ADD wkhtmltopdf/wkhtmltopdf /usr/bin/wkhtmltopdf
RUN chmod 755 /usr/bin/wkhtmltopdf


#RUN composer install -o && /bin/sh -c composer config -g
