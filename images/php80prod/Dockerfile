FROM dmitriikoziuk/php-8.0.9-fpm:1.0.0

MAINTAINER Dmitrii Kozyuk <dmitriikoziuk@gmail.com>

ARG username
ARG userid
ARG usergroupid

RUN groupadd -g $usergroupid $username \
    && useradd -r -d /var/www -s /bin/bash -g $username -G sudo -u $userid $username \
    && chown $username:$username /tmp/xhprof

USER $username:$username

WORKDIR /var/www

CMD ["php-fpm"]
