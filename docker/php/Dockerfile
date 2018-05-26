FROM php:7.2-fpm

RUN apt-get update \
    && apt-get install -y git curl wget unzip

# Set TIMEZONE
RUN rm /etc/localtime \
    && ln -s /usr/share/zoneinfo/Europe/Paris /etc/localtime \
    && "date"

# Install OPCACHE extension
RUN docker-php-ext-install opcache

# Install INTL extension
RUN apt-get install -y libicu-dev \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl

# Install APCU extension
RUN pecl install apcu \
    && docker-php-ext-enable apcu

## Install GD extension
RUN apt-get update \
    && apt-get install -y \
    libpng-dev \
    libfreetype6-dev \
    libjpeg-dev \
    libxpm-dev \
    libxml2-dev \
    libxslt-dev \
    libwebp-dev \
    && docker-php-ext-configure gd \
    --with-freetype-dir=/usr/include/ \
    --with-jpeg-dir=/usr/include/ \
    --with-xpm-dir=/usr/include/ \
    --with-webp-dir=/usr/include/ \
    && docker-php-ext-install gd

# Install IMAGICK extension
RUN apt-get update \
    && apt-get install -y libmagickwand-dev --no-install-recommends \
    && pecl install imagick \
    && docker-php-ext-enable imagick

# Install EXIF extension
RUN docker-php-ext-install exif

# Install MYSQLI extension
RUN docker-php-ext-install mysqli

# Install PDO MYSQL extension
RUN docker-php-ext-install pdo_mysql

# Install ZIP extension
RUN apt-get install -y libzip-dev zip \
  && docker-php-ext-configure zip --with-libzip \
  && docker-php-ext-install zip

# Install XSL extension
RUN apt-get install -y libxslt-dev \
    && docker-php-ext-install xsl

# Install SOAP extension
RUN docker-php-ext-install soap

# Install BCMATH extension
RUN docker-php-ext-install bcmath

# Install GMP extension
RUN apt-get install -y libgmp-dev \
    && docker-php-ext-install gmp

# Install XDEBUG extension
RUN pecl install xdebug \
    && docker-php-ext-enable xdebug

# Install MONGODB extension
RUN apt-get install -y autoconf pkg-config libssl-dev \
    && pecl install mongodb \
    && docker-php-ext-enable mongodb

# Install COMPOSER
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install BLACKFIRE PROBE
#RUN version=$(php -r "echo PHP_MAJOR_VERSION.PHP_MINOR_VERSION;") \
#    && curl -A "Docker" -o /tmp/blackfire-probe.tar.gz -D - -L -s https://blackfire.io/api/v1/releases/probe/php/linux/amd64/$version \
#    && tar zxpf /tmp/blackfire-probe.tar.gz -C /tmp \
#    && mv /tmp/blackfire-*.so $(php -r "echo ini_get('extension_dir');")/blackfire.so \
#    && printf "extension=blackfire.so\nblackfire.agent_socket=tcp://blackfire:8707\n" > $PHP_INI_DIR/conf.d/blackfire.ini

# Install BLACKFIRE AGENT
#RUN mkdir -p /tmp/blackfire \
#    && curl -A "Docker" -L https://blackfire.io/api/v1/releases/client/linux_static/amd64 | tar zxp -C /tmp/blackfire \
#    && mv /tmp/blackfire/blackfire /usr/bin/blackfire \
#    && rm -Rf /tmp/blackfire

# Set PROJECT USER
RUN useradd -ms /bin/bash project
USER project
WORKDIR /project

COPY conf/php-fpm.conf /etc/php-fpm.conf
COPY conf/php.ini /usr/local/etc/php/conf.d/100-php.ini
