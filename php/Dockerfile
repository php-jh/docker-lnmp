FROM deepoo/mj_php72:v5

# GIT 配置
ARG XDEBUG_REMOTE_HOST=
ARG GIT_LOGIN_ACCOUNT=test
ARG GIT_LOGIN_TOKEN=test
ARG GIT_USER_NAME=test
ARG GIT_USER_EMAIL=test@majorbio.com
RUN git config --global user.name "${GIT_USER_NAME}" && \
    git config --global user.email "${GIT_USER_EMAIL}" && \
    git config --global core.fileMode false

RUN mkdir -p /home/www-data
RUN usermod -d /home/www-data www-data
RUN echo "https://${GIT_LOGIN_ACCOUNT}:${GIT_LOGIN_TOKEN}@git.i-sanger.com" > /home/www-data/.git-credentials
RUN echo "[user]\n\tname = ${GIT_USER_NAME}\n\temail = ${GIT_USER_EMAIL}\n[credential]\n\thelper = store" > /home/www-data/.gitconfig
RUN chown -R www-data:www-data /home/www-data
RUN git config --global credential.helper store

# xdebug.ini 配置
RUN echo "xdebug.idekey=PHPSTORM\nxdebug.remote_enable=on\nxdebug.remote_host=${XDEBUG_REMOTE_HOST} \nxdebug.remote_port=9001\nxdebug.remote_handler=dbgp" > /usr/local/etc/php/conf.d/xdebug.ini

# 字体
ADD fonts/SIMSUN.TTC /usr/share/fonts

WORKDIR /var/www

CMD ["php-fpm"]

EXPOSE 9000