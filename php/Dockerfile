# ----------------------
# The FPM base container
# ----------------------
FROM php:7.2-fpm as dev

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

RUN docker-php-ext-install zip bz2 mbstring pdo pdo_pgsql pcntl soap && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install gd && \
    docker-php-ext-enable mcrypt

ARG DOCKER_ARM
RUN if [ ${DOCKER_ARM} = "true" ] ; then \
    wget -nv -O /tmp/wkhtmltox.deb https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6-1/wkhtmltox_0.12.6-1.stretch_arm64.deb && \
        apt-get -qy install /tmp/wkhtmltox.deb ; \
else \
    wget -nv -O /tmp/wkhtmltox.deb https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6-1/wkhtmltox_0.12.6-1.stretch_amd64.deb && \
        apt-get -qy install /tmp/wkhtmltox.deb ; \
fi

COPY --from=composer:1.10.16 /usr/bin/composer /usr/local/bin/composer

RUN php /usr/local/bin/composer global require hirak/prestissimo --no-plugins --no-scripts

WORKDIR /var/www/html

COPY ./www.conf /usr/local/etc/php-fpm.d/www.conf

CMD ["/bin/sh", "-c", "php-fpm"]