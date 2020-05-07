FROM dmitriikoziuk/php-7.4.5-fpm-dev:latest

MAINTAINER Dmitrii Kozyuk <dmitriikoziuk@gmail.com>

ARG username
ARG userid
ARG usergroupid

ENV PHP_IDE_CONFIG="serverName=php74dev"

RUN groupadd -g $usergroupid $username \
    && useradd -r -d /var/www -s /bin/bash -g $username -G sudo -u $userid $username \
    && chown $username:$username /tmp/xhprof

USER $username:$username

WORKDIR /var/www

CMD ["php-fpm"]
