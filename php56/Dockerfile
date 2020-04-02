FROM php:5.6-fpm

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


# php 配置文件
ADD www.conf /usr/local/etc/php-fpm.d/www.conf

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