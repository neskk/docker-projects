
# Docker Templates

Docker templates for development environments.

## Docker commands

### Build the project

> docker-compose build

> docker-compose up -d

### Shutdown and cleanup

Preserve database volume:
> docker-compose down

Remove the containers, default network, and the **database volume**:
> docker-compose down --volumes

### Access a container

> docker exec -it CONTAINER /bin/bash

> docker logs -f CONTAINER

----

## LAMP Setup - Linux Apache MySQL PHP

- [Containerize LAMP stack with Docker](https://www.cloudreach.com/en/resources/blog/containerize-this-how-to-use-php-apache-mysql-within-docker-containers/)

### Credentials

Credentials are defined on an `.env` file.
This file is read by docker-compose which then sets the environment variables for each container.

### PHP Custom Configuration

The `php.ini` file present in the template allows you to easily override PHP directives.

### Similar projects / images
- https://github.com/mattrayner/docker-lamp
- https://github.com/fauria/docker-lamp
- https://github.com/matriphe/docker-alpine-php
- https://github.com/ulsmith/alpine-apache-php7
- https://github.com/ulsmith/debian-apache-php

----

## WordPress Setup

- [WordPress Docker Images](https://github.com/docker-library/wordpress)
- [Official WordPress Docker Guide](https://docs.docker.com/compose/wordpress/)
- [Docker + WordPress Setup](https://davidyeiser.com/tutorials/docker-wordpress-theme-setup)

Launch the containers and navigate to http://localhost:8000/ to finish the WordPress setup.

### Credentials

Credentials are defined on an `.env` file.
This file is read by docker-compose which then sets the environment variables for each container.

### PHP Custom Configuration

The `php.ini` file present in the template allows you to easily override PHP directives.

----

## [PHP-Apache Image](https://hub.docker.com/_/php)

### How to install more PHP extensions

We provide the helper scripts `docker-php-ext-configure`, `docker-php-ext-install`, and `docker-php-ext-enable` to more easily install PHP extensions.
> docker-php-ext-install mysqli

### Check PHP modules

> php -m

> php -i

### Check GD extension

> php -r 'print_r(gd_info());'


## [MySQL Image](https://hub.docker.com/_/mysql)

### Creating database dumps

Most of the normal tools will work, although their usage might be a little convoluted in some cases to ensure they have access to the mysqld server. A simple way to ensure this is to use docker exec and run the tool from the same container, similar to the following:

> docker exec CONTAINER sh -c 'exec mysqldump --all-databases -uroot -p"$MYSQL_ROOT_PASSWORD"' > /some/path/on/your/host/all-databases.sql

### Restoring data from dump files

For restoring data. You can use docker exec command with -i flag, similar to the following:

> docker exec -i CONTAINER sh -c 'exec mysql -uroot -p"$MYSQL_ROOT_PASSWORD"' < /some/path/on/your/host/all-databases.sql


## [WordPress Image](https://hub.docker.com/_/wordpress/)

This image does not provide any additional PHP extensions or other libraries, even if they are required by popular plugins (e.g. it cannot send e-mails).
There are an infinite number of possible plugins, and they potentially require any extension PHP supports.
Including every PHP extension that exists would dramatically increase the image size.

If you need additional PHP extensions, you'll need to create your own image.
The [documentation of the php image](https://hub.docker.com/_/php) explains how to compile additional extensions.
Additionally, the [WordPress Dockerfile](https://github.com/docker-library/wordpress) has an example of doing this.
