FROM php:7.1-fpm

RUN apt-get update && apt-get install -y \
    unzip

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && composer --version

# Set timezone
RUN rm /etc/localtime && ln -s /usr/share/zoneinfo/Europe/Paris /etc/localtime && date

# Type docker-php-ext-install to see available extensions
RUN docker-php-ext-install pdo pdo_mysql

# install xdebug
RUN pecl install xdebug && \
    docker-php-ext-enable xdebug && \
    { \
        echo "xdebug.remote_enable=1"; \
        echo "xdebug.remote_connect_back=1"; \
        echo "xdebug.idekey=\"PHPSTORM\""; \
        "xdebug.remote_port=9001"; \
    } > /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

# user
RUN useradd -ms /bin/bash symfony
USER symfony

WORKDIR /symfony

COPY conf/php-fpm.conf /etc/php-fpm.conf
COPY conf/php.ini /usr/local/etc/php/conf.d/100-php.ini
