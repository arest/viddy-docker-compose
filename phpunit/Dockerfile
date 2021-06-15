FROM php:7.2-cli

RUN apt-get update
RUN apt-get install -y --no-install-recommends \
    software-properties-common \
    gpg \
    dirmngr \
    gpg-agent

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    imagemagick \
    libpq-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    libbz2-dev \
    libxml2-dev \
    libglu1 \
    cron \
    git \
    unzip \
    procps
    
RUN pecl channel-update pecl.php.net \
    && pecl install apcu mcrypt-1.0.1

RUN docker-php-ext-install zip bz2 mbstring pdo pdo_pgsql soap && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install gd && \
    docker-php-ext-enable mcrypt

WORKDIR /var/www/html

CMD ["/bin/sh", "-c", "vendor/bin/phpunit"]