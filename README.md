Docker Symfony
==============

**Starting point** Docker configuration for **Symfony** and other PHP projects (*drupal*, *wordpress*...). 

### What's inside ?

| CONTAINER | NOTES |
|--|--|
| **PHP 7.2** | enabled |
| **NGINX 1.14** | enabled |
| **MYSQL 5.7** | enabled |
| **NODE 8.12** | enabled |
| **MAILDEV** | enabled |

| CONTAINER | NOTES |
|--|--|
| HTTPD 2.4 | optional, disabled |
| BLACKFIRE | optional, disabled |
| PHPMYADMIN | optional, disabled |

### How to use this repository ?

 1. **Copy** this repository files and directory at the root of your php project.
 2. **Copy** the *docker-compose.override.yml.dist* file to *docker-compose.override.yml*.
 3. **Add** the *docker-compose.override.yml* file to *.gitignore*.

### Docker commands cheatsheet
    
#### Build containers (and pull latest images)

```bash
$ docker-compose build --pull
```

#### Start containers (and build if needed)

```bash
$ docker-compose up --build
```

#### Stop running containers

```bash
$ docker-compose stop
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

### Web access through NGINX

    http://localhost (no extra step needed)
    http://project.tld (add an entry "127.0.0.1 project.tld" to the host /etc/hosts file)

### Web access through Apache httpd

Uncomment the **httpd section** of the *docker-compose.yml* file and adapt the mapped ports in the *docker-compose.override.yml* file.

### Maildev UI access

    http://localhost:1080

### Xdebug usage

Xdebug is enabled by default. However, it is necessary to use a browser's extension to catch it.
Example of extensions for Google Chrome: [xdebug helper](https://chrome.google.com/webstore/detail/xdebug-helper/eadndfjplgieldjbigjakmdgkmoaaaoc)

### Blackfire usage

Configure your blackfire credentials in the *docker/.env* file. 
Uncomment the **blackfire section** in the *docker-compose.yml* and *docker/php/Dockerfile* files.
See https://blackfire.io/docs/integrations/docker for more informations.

#### From host

```bash
$ docker-compose exec blackfire blackfire curl http://nginx
```    

#### From container

```bash
$ docker-compose exec php /bin/bash
$ blackfire run php script.php
$ blackfire curl http://nginx
```

### phpMyAdmin 

A tool like MySQL Workbench would be better but if you really want it uncomment the **phpmyadmin section** in the *docker-compose.yml* file.

    http://localhost:8080
