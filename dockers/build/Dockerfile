FROM php:7.1-fpm-alpine

ENV PATH /root/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/local/lib/node_modules

RUN apk --update add \
    ca-certificates \
    bash \
    curl \
    tar \
    xz \
    g++ \
    gcc \
    file \
    make \
    re2c \
    libc-dev \
    pkgconf \
    autoconf \
    dpkg dpkg-dev \
    libressl \
    libmcrypt \
    python2 \
    py-setuptools

# Python install
RUN if [[ ! -e /usr/bin/python ]]; then ln -sf /usr/bin/python2.7 /usr/bin/python; fi \
    && if [[ ! -e /usr/bin/python-config ]]; then ln -sf /usr/bin/python2.7-config /usr/bin/python-config; fi \
    && if [[ ! -e /usr/bin/easy_install ]]; then ln -sf /usr/bin/easy_install-2.7 /usr/bin/easy_install; fi \
    && easy_install pip \
    && pip install --upgrade pip \
    && if [[ ! -e /usr/bin/pip ]]; then ln -sf /usr/bin/pip2.7 /usr/bin/pip; fi

# NPM and dependencies
RUN apk --update add nodejs nodejs-npm yarn

RUN npm install npm@latest -g

RUN yarn global add \
    node-sass \
    gulp

RUN apk update && apk add -u yarn

# RUN npm install > $EXTRA_NPM_PACKAGES

# Install PHP ( for composer )
RUN apk --update add \
    libmcrypt \
    libmcrypt-dev \
    libffi-dev \
    icu-dev

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

WORKDIR /var/www/current
