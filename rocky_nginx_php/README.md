# minwork/centos-apache-php

![docker stars](https://img.shields.io/docker/stars/minwork/rocky-nginx-php.svg) ![docker pulls](https://img.shields.io/docker/pulls/minwork/rocky-nginx-php.svg)  ![tag-php 7.4](https://img.shields.io/badge/tag-php74-brightgreen.svg)![tag-php 8.2](https://img.shields.io/badge/tag-php82-brightgreen.svg)

1. Specification:
    - Rocky Linux 9.2
    - Nginx 1.10
    - PHP (7.4 and 8.2)
        - The php version can be selected as a tag.

1. Docker Pull Command
    - docker pull minwork/rocky-nginx-php:php82

1. Use
    1. The docutment root of this docker image is set to **/var/www/approot**. This dirctory set to **AllowOverride All** and **Allow from all**. And **/var/www/approot** is set to **VOLUME**.
    1. Simply, mount the PHP project directory in this folder.
    1. If necessary, connect to the container and make additional settings.
        - Environment variables, project config, timezone and etc...
        - Or [jwilder/nginx-proxy](https://hub.docker.com/r/jwilder/nginx-proxy/)

1. Contents of dockerfile:
    - Creates from the rockylinux:9.2 Docker image.
    - Install PHP (7.4, 8.2)
    - Set */etc/php-fpm.d/www.conf*
        ```
        user = nginx
        group = nginx
        listen = /run/php-fpm.sock
        ```
    - Set */etc/php.ini*
        ```
        date.timezone "Asia/Seoul"
        ```
    - Set */etc/nginx/nginx.conf*
        ```
        root /var/www/approot;
        ```
    - Set **EXPOSE**
        - 80 443
    - Add **ENV**
        - 'VIRTUAL_HOST'. It use 'nginx-proxy' container.
            - [jwilder/nginx-proxy](https://hub.docker.com/r/jwilder/nginx-proxy/)
    - Set **VOLUME**
        - '/var/www/approot'
    - Set **CMD**
        - run script to start php-fpm and nginx, at container is start or restart.
