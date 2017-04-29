symfony + docker starter
========================

PHP 7.1 + MYSQL 5.7 + NGINX 1.11 (+ MAILDEV + PAGESPEED)

### important files and directories

    ./docker
    ./docker-compose.yml
    
    ./app/config/parameters.yml.dist

### docker commands
    
    docker-compose build
    docker-compose up
    docker-compose up -d
    
    docker-compose stop
    docker-compose rm -v

### execute php commands (from php container)

    docker-compose exec php /bin/bash
    composer install -o

### execute php commands (from host)
    
    docker-compose exec php composer install -o

### mysql management (from mysql container)
    
    docker-compose exec mysql /bin/bash
    mysql -uroot -p

### mysql management (from host)
    
    mysql -uroot -p --host=127.0.0.1 --port=3306

### web access

    http://localhost
    http://symfony.dock

### nginx + pagespeed module

Uncomment the nginx_pagespeed service configuration block and modify the mapped port to suit your needs.

    http://localhost:81

### maildev access

    http://localhost:1080

### phpmyadmin access

A tool like MySQL Workbench would be better in my opinion but if you really want it uncomment the phpmyadmin section in the docker-compose.yml

    http://localhost:8080
