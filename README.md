Docker PHP / Symfony starter
============================ 

PHP 7.1 + MYSQL 5.7 + NGINX 1.12 ( + MAILDEV + BLACKFIRE + NODEJS + YARN + APACHE HTTPD 2.4 + NGINX PAGESPEED + PHPMYADMIN).

### usage

Copy this repository files and directory at the root of the symfony project. 
Don't forget to copy the docker/.env.dist file to docker/.env.

### docker commands
    
    # start (and build) containers
    docker-compose up
    docker-compose up --build
    docker-compose up -d
    
    # stop running containers
    docker-compose stop
    
    # cleanup containers and volumes
    docker-compose rm -v
    
    # display container logs
    docker-compose logs mysql
    
    # go into container shell
    docker-compose exec mysql /bin/bash

### execute php commands

    # from inside php container
    docker-compose exec php /bin/bash
    composer install -o

    # from host
    docker-compose exec php composer install -o

### mysql interaction
    
    # from inside mysql container
    docker-compose exec mysql /bin/bash
    mysql -uroot -p

    # from host (mysql client required)
    mysql -uroot -p --host=127.0.0.1 --port=3306
    docker-compose exec mysql sh -c 'exec mysqldump -u"$MYSQL_USER" -p"$MYSQL_PASSWORD" "$MYSQL_DATABASE"' > ./dump.sql

### web access

    http://localhost
    http://symfony.dock (by adding an entry "127.0.0.1 symfony.dock" to the host /etc/hosts file)

### blackfire usage

Configure your blackfire credentials in the docker/.env file. 
Uncomment the blackfire part in the docker-compose-yml and docker/php/Dockerfile files.
See https://blackfire.io/docs/integrations/docker for more informations.

    # from host
    docker-compose exec blackfire blackfire curl http://nginx
    
    # from php container
    docker-compose exec php /bin/bash
    blackfire run php script.php
    blackfire curl http://nginx

### maildev access

    http://localhost:1080

### apache httpd

Uncomment the httpd sections of the docker-compose.yml file and adapat the mapped ports in the docker-compose.override.yml file.

### nginx + pagespeed module

Uncomment the nginx_pagespeed service configuration block and modify the mapped port to suit your needs.

    http://localhost:81

### phpmyadmin access

A tool like MySQL Workbench would be better but if you really want it uncomment the phpmyadmin section in the docker-compose.yml

    http://localhost:8080
