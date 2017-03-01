symfony + docker starter
========================

PHP 7.1 + NGINX 1.11 + MYSQL 5.7 (+ MAILDEV)

### fles

    ./docker
    ./docker-compose.yml

### commands
    
    docker-compose build
    docker-compose up
    docker-compose up -d
    
    docker-compose stop
    docker-compose rm -v

### web

    http://localhost:80
    http://symfony.dock

### php 

    docker-compose exec php /bin/bash

### mysql
    
    mysql -uroot -proot --host=127.0.0.1 --port=3306

### maildev

    http://localhost:1080
