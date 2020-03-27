FROM php:5.6-fpm

# php 配置文件
ADD www.conf /usr/local/etc/php-fpm.d/www.conf

WORKDIR /var/www

CMD ["php-fpm"]

EXPOSE 9000