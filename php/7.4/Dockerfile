FROM php:7.4-fpm-alpine

MAINTAINER tonyyb <dev@tony.botalla.me>

RUN apk add --no-cache --virtual .build-deps \
        $PHPIZE_DEPS \
        curl-dev \
        imagemagick-dev \
        freetype-dev  \
        gmp-dev \
        libtool \
        libxml2-dev \
        postgresql-dev \
        sqlite-dev \
        libpng-dev \
        libmcrypt-dev \
        libjpeg-turbo-dev \
        zlib-dev \
    && apk add --no-cache \
        curl \
        git \
        imagemagick \
        mysql-client \
        openssh-client \
        postgresql-libs \
        libintl \
        icu \
        icu-dev \
        nodejs \
        nodejs-npm \
        yarn \
        libzip-dev \
    && apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/community/ --allow-untrusted \
        gnu-libiconv \
    && pecl install imagick \
        redis \
    && docker-php-ext-enable imagick redis \
    && docker-php-ext-configure exif \
    && docker-php-ext-install \
        bcmath \
        exif \
        gd \
        gmp \
        intl \
        mysqli \
        pcntl \
        pdo_mysql \
        pdo_pgsql \
        pdo_sqlite \
        pgsql \
        soap \
        tokenizer \
        zip \
        xml \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && curl -s https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer \
    && apk del -f .build-deps

# Configure non-root user.
RUN apk add --no-cache bash
RUN apk --no-cache add shadow
ARG PUID=1000
ENV PUID ${PUID}
ARG PGID=1000
ENV PGID ${PGID}

RUN groupmod -o -g ${PGID} www-data && \
    usermod -o -u ${PUID} -g www-data www-data

RUN echo 'alias pamfs="php artisan migrate:fresh --seed --drop-views"' >> /home/www-data/.bashrc
RUN echo 'alias pamf="php artisan migrate:fresh"' >> /home/www-data/.bashrc
RUN echo 'alias pads="php artisan db:seed"' >> /home/www-data/.bashrc
RUN echo 'alias pacc="php artisan cache:clear"' >> /home/www-data/.bashrc
RUN echo 'alias pahm="php artisan ide-helper:models"' >> /home/www-data/.bashrc
RUN echo 'alias pahe="php artisan ide-helper:eloquent"' >> /home/www-data/.bashrc
RUN echo 'alias pahg="php artisan ide-helper:generate"' >> /home/www-data/.bashrc
RUN echo 'alias pa="php artisan"' >> /home/www-data/.bashrc
RUN echo 'alias gb="git branch"' >> /home/www-data/.bashrc
RUN echo 'alias gco="git checkout"' >> /home/www-data/.bashrc
RUN echo 'alias gcob="git checkout -b"' >> /home/www-data/.bashrc
RUN echo 'alias gs="git status"' >> /home/www-data/.bashrc
RUN echo 'alias ga="git add ."' >> /home/www-data/.bashrc
RUN echo 'alias gc="git commit"' >> /home/www-data/.bashrc
RUN echo 'alias gp="git pull"' >> /home/www-data/.bashrc
RUN echo 'alias gpo="git push origin"' >> /home/www-data/.bashrc
RUN echo 'alias gl="git log"' >> /home/www-data/.bashrc
RUN echo 'alias gls="git log --stat"' >> /home/www-data/.bashrc
RUN echo 'alias gfo="git fetch origin"' >> /home/www-data/.bashrc

WORKDIR /var/www






