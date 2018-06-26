FROM php:7.1-fpm-alpine

ENV PATH /root/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

ENV TZ=Europe/Paris
ENV LOCALE=fr_FR.UTF-8

RUN apk --update add \
    openssl \
    openssh \
    bash \
    zip \
    unzip \
    bzip2 \
    tzdata \
    git \
    sshpass

# Set timezone
RUN rm /etc/localtime
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN "date"

# Set locale
# RUN /usr/sbin/locale-gen $LOCALE
# RUN sed -i -e "s/# $LOCALE UTF-8/$LOCALE UTF-8/" /etc/locale.gen

# Install language pack
RUN apk --no-cache add ca-certificates wget && \
    wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://raw.githubusercontent.com/sgerrand/alpine-pkg-glibc/master/sgerrand.rsa.pub && \
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.25-r0/glibc-2.25-r0.apk && \
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.25-r0/glibc-bin-2.25-r0.apk && \
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.25-r0/glibc-i18n-2.25-r0.apk && \
    apk add glibc-bin-2.25-r0.apk glibc-i18n-2.25-r0.apk glibc-2.25-r0.apk

ENV LANG=$LOCALE \
    LANGUAGE=$LOCALE \
    LC_CTYPE=$LOCALE \
    LC_NUMERIC=$LOCALE \
    LC_TIME=$LOCALE \
    LC_COLLATE=$LOCALE \
    LC_MONETARY=$LOCALE \
    LC_MESSAGES=$LOCALE \
    LC_PAPER=$LOCALE \
    LC_NAME=$LOCALE \
    LC_ADDRESS=$LOCALE \
    LC_TELEPHONE=$LOCALE \
    LC_MEASUREMENT=$LOCALE \
    LC_IDENTIFICATION=$LOCALE \
    LC_ALL=$LOCALE

# Install PHP extensions dependencies
RUN apk add \
    libxml2 \
    libxml2-dev \
    libmcrypt \
    libmcrypt-dev \
    libffi-dev \
    libxslt \
    libxslt-dev \
    icu-dev

# Configure and install PHP extensions
RUN docker-php-ext-install -j$(nproc) iconv mcrypt opcache intl xsl json session simplexml xml zip pdo_mysql pdo mysqli

# Install GD with png, jpg libs
RUN apk add --no-cache freetype libpng libjpeg-turbo freetype-dev libpng-dev libjpeg-turbo-dev && \
    docker-php-ext-configure gd \
    --with-gd \
    --with-freetype-dir=/usr/include/ \
    --with-png-dir=/usr/include/ \
    --with-jpeg-dir=/usr/include/ && \
    NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) && \
    docker-php-ext-install -j${NPROC} gd && \
    apk del --no-cache freetype-dev libpng-dev libjpeg-turbo-dev

# Configure PHP Limits
RUN echo -e \
        "date.timezone=$TZ\n" \
        'file_uploads=On\n' \
        'memory_limit=-1\n' \
        'upload_max_filesize=8M\n' \
        'post_max_size=20M\n' \
        'max_execution_time=0\n' \
        'max_input_time=-1\n' \
        'expose_php=Off\n' \
    > /usr/local/etc/php/conf.d/php_app_configuration.ini

# Sendmail
RUN apk add msmtp
RUN ln -sf /usr/bin/msmtp /usr/sbin/sendmail

WORKDIR /var/www/current
