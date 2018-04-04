
Docker PHP / Symfony starter
============================

**Starting point** Docker configuration for PHP projects (*symfony*, *drupal*, *wordpress*...). 

### What's inside ?

| CONTAINER | NOTES |
|--|--|
| **PHP 7.1** | enabled |
| **NGINX 1.12** | enabled |
| MYSQL 5.7 | enabled |
| MAILDEV | enabled |

| CONTAINER | NOTES |
|--|--|
| HTTPD 2.4 | optional, disabled |
| NGINX PAGESPEED | optional, disabled |
| BLACKFIRE | optional, disabled |
| PHPMYADMIN | optional, disabled |

### How to use this repository ?

 1. **Copy** this repository files and directory at the root of your php project.
 2. **Copy** the *docker-compose.override.yml.dist* to *docker-compose.override.yml* and the  *docker/.env.dist* file to *docker/.env*.
 3. **Add** the *docker-compose.override.yml* and *docker/.env* files to *.gitignore*.

### Docker commands cheatsheet
    
#### Start containers (and build if needed)
```bash
$ docker-compose up --build
```
#### Stop and remove containers, networks and volumes
```bash
$ docker-compose down --volumes --remove-orphans
```
#### Display and follow logs of a container
```bash
$ docker-compose logs -f mysql
```
#### Get an interactive prompt for a container
```bash
$ docker-compose exec mysql /bin/bash
```
### Interact with PHP

#### From container
```bash
$ docker-compose exec php /bin/bash
$ composer install
```
#### From host
```bash
$ docker-compose exec php composer install
```
### Interact with MySQL
    
#### From container
```bash
$ docker-compose exec mysql /bin/bash
$ mysql -uroot -p
```
#### From host (mysql client required)
```bash
$ mysql -uroot -p --host=127.0.0.1 --port=3306
$ docker-compose exec mysql sh -c 'exec mysqldump -u"$MYSQL_USER" -p"$MYSQL_PASSWORD" "$MYSQL_DATABASE"' > ./dump.sql
```
### Web access

    http://localhost (no extra step needed)
    http://project.dock (add an entry "127.0.0.1 project.dock" to the host /etc/hosts file)

### Maildev access

    http://localhost:1080

### Blackfire usage

Configure your blackfire credentials in the *docker/.env* file. 
Uncomment the **blackfire section** in the *docker-compose.yml* and *docker/php/Dockerfile* files.
See https://blackfire.io/docs/integrations/docker for more informations.

### xdebug usage
Xdebug is enabled by default. However, it is necessary to use a browser's extension to catch it.
Example of extensions for Google Chrome: [xdebug helper](https://chrome.google.com/webstore/detail/xdebug-helper/eadndfjplgieldjbigjakmdgkmoaaaoc)

#### From host
```bash
docker-compose exec blackfire blackfire curl http://nginx
```    
#### From container
```bash
$ docker-compose exec php /bin/bash
$ blackfire run php script.php
$ blackfire curl http://nginx
```
### Apache httpd

Uncomment the **httpd section** of the *docker-compose.yml* file and adapt the mapped ports in the *docker-compose.override.yml* file.

### Nginx + PageSpeed module

Uncomment the **nginx_pagespeed section** of the *docker-compose.yml* file and modify the mapped port to suit your needs.

    http://localhost:81

### phpMyAdmin 

A tool like MySQL Workbench would be better but if you really want it uncomment the **phpmyadmin section** in the *docker-compose.yml* file.

    http://localhost:8080
