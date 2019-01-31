# Docker Setup for Typo3 9 LTS

This repository exists, because MAMP and XAMPP wouldn't let me install Typo3. But maybe Typo3 didn't want me to install it? (:

This setup uses the official PHP 7.2 apache images. It has added unicode setup for the MariaDB and configuration for the PHP Apache container to install composer, install/configure the imagemagick extension and also enable other php extensions.

This runs well on Win10.

## Installation

Install docker and docker-compose. Share the device your keep your source files in the docker settings. Run `$ docker-compose up` to create the containers.

## MariaDB

MariaDB is running as a container with a volume mount. While running:

Databasedump:
```bash
$ docker exec CONTAINER /usr/bin/mysqldump -u root --password=root DATABASE > backup.sql
```

Load Database:
```bash
$ cat backup.sql | docker exec -i CONTAINER /usr/bin/mysql -u root --password=root DATABASE
```

## Composer

To install Typo3 or any of its packages it's recommended to use composer. Use it by:

1. `$ docker container ls` and grabbing the id of the php-apache container.
2. `$ docker exec -it <containerId> bash` into the shell, which takes you to the `/var/www/html` folder on the apache container.
3. `$ cd /var/www/typo3` into your typo3 source, where you can install typo3 using composer `$ composer create-project typo3/cms-base-distribution . ^9` or install other packages.