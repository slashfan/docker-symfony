symfony + docker starter
========================

PHP 7.1 + MYSQL 5.7 + NGINX 1.11 (+ MAILDEV)

### important files and directories

    ./docker
    ./docker-compose.yml

### docker commands
    
    docker-compose build
    docker-compose up
    docker-compose up -d
    
    docker-compose stop
    docker-compose rm -v

### execute php commands (from php container)

    docker-compose exec php /bin/bash

### mysql management (from host)
    
    mysql -uroot -proot --host=127.0.0.1 --port=3306

### web access

    http://localhost:80
    http://symfony.dock

### maildev access

    http://localhost:1080
