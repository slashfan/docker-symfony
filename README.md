symfony + docker starter
========================

PHP 7.1 + MYSQL 5.7 + NGINX 1.11 (+ BLACKFIRE + MAILDEV + PHPMYADMIN + PAGESPEED)

### usage

Copy this repository files and directory at the root of the symfony project. Don't forget to copy the .docker/.env.dist file to .docker/.env.

### docker commands
    
    # start
    docker-compose up
    docker-compose up -d
    
    # stop
    docker-compose stop
    
    # cleanup
    docker-compose rm -v
    
    # logs
    docker-compose logs mysql

### execute php commands

    # from php container
    docker-compose exec php /bin/bash
    composer install -o

    # from host
    docker-compose exec php composer install -o

### mysql interaction
    
    # from mysql container
    docker-compose exec mysql /bin/bash
    mysql -uroot -p

    # from host
    mysql -uroot -p --host=127.0.0.1 --port=3306
    docker-compose exec mysql sh -c 'exec mysqldump -u"$MYSQL_USER" -p"$MYSQL_PASSWORD" "$MYSQL_DATABASE"' > ./dump.sql

### web access

    http://localhost
    http://symfony.dock

### blackfire usage

Configure your blackfire credentials in the .docker/.env file. See https://blackfire.io/docs/integrations/docker for more informations.

    # from host
    docker-compose exec blackfire blackfire curl http://nginx
    
    # from php container
    docker-compose exec php /bin/bash
    blackfire run php script.php
    blackfire curl http://nginx

### maildev access

    http://localhost:1080

### nginx + pagespeed module

Uncomment the nginx_pagespeed service configuration block and modify the mapped port to suit your needs.

    http://localhost:81

### phpmyadmin access

A tool like MySQL Workbench would be better in my opinion but if you really want it uncomment the phpmyadmin section in the docker-compose.yml

    http://localhost:8080
