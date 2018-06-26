FROM nginx:1.15-alpine

ENV PATH /root/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

ENV TZ=Europe/Paris
ENV PHP_HOST=php
ENV PHP_PORT=9000
ENV PHP_USER_UID=82

# Set timezone
RUN apk --update add tzdata bash
RUN rm /etc/localtime
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN "date"

# Configure
ADD nginx.conf /etc/nginx/
ADD app.conf /etc/nginx/conf.d/

RUN echo "upstream php-upstream { server ${PHP_HOST}:${PHP_PORT}; }" > /etc/nginx/conf.d/upstream.conf

RUN set -x ; \
    addgroup -g $PHP_USER_UID -S www-data ; \
    adduser -u $PHP_USER_UID -D -S -H -G www-data www-data && exit 0 ; exit 1

RUN apk --no-cache add shadow && usermod -u $PHP_USER_UID www-data

EXPOSE 443
