# minwork/centos-apache-php

![docker stars](https://img.shields.io/docker/stars/minwork/centos-apache-php.svg) ![docker pulls](https://img.shields.io/docker/pulls/minwork/centos-apache-php.svg)  ![tag-php 5.3](https://img.shields.io/badge/tag-php53-brightgreen.svg) ![tag-PHP 5.6](https://img.shields.io/badge/tag-php56-brightgreen.svg) ![tag-PHP 7.1](https://img.shields.io/badge/tag-php71-brightgreen.svg)

1. Specification:
    - CentOS 6.10
    - Apache 2.2
    - PHP (5.3 or 5.6 or 7.1)
        - The php version can be selected as a tag.

1. Docker Pull Command
    - docker pull minwork/centos-apache-php:php56
    - docker pull minwork/centos-apache-php:php53
    - docker pull minwork/centos-apache-php:php71

1. Use
    1. The docutment root of this docker image is set to **/var/local_shared**. This dirctory set to **AllowOverride All** and **Allow from all**. And **/var/local_shared** is set to **VOLUME**.
    1. Simply, mount the PHP project directory in this folder.
    1. If necessary, connect to the container and make additional settings.
        - Environment variables, project config, timezone and etc...
        - Or [jwilder/nginx-proxy](https://hub.docker.com/r/jwilder/nginx-proxy/)

1. Contents of dockerfile:
    - Creates from the centos:6.10 Docker image.
    - Install PHP (5.3 or 5.6 or 7.1)
    - Set httpd.conf
        - DocumentRoot '/var/local_shared'.
        - '/var/local_shared' directory
            - AllowOverride All
            - Allow from all
    - Set php.ini
        - timezone 'Asia/Seoul'
    - Set **EXPOSE**
        - 80 443
    - Add **ENV**
        - 'VIRTUAL_HOST'. It use 'nginx-proxy' container.
            - [jwilder/nginx-proxy](https://hub.docker.com/r/jwilder/nginx-proxy/)
    - Set **VOLUME**
        - '/var/local_shared'
    - Set **CMD**
        - run script to start httpd at container is start or restart.
