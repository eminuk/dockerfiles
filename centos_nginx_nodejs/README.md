# minwork/centos-apache-php

![docker stars](https://img.shields.io/docker/stars/minwork/centos-nginx-nodejs.svg) ![docker pulls](https://img.shields.io/docker/pulls/minwork/centos-nginx-nodejs.svg) ![tag-latest](https://img.shields.io/badge/tag-latest-brightgreen.svg)

1. Specification:
    - CentOS 6.10
    - Nginx 1.10
    - Node.js 8.12

1. Docker Pull Command
    - docker pull minwork/centos-nginx-nodejs:latest

1. Use
    1. Mount the node.js project in **VOLUME** directory(**/var/local_shared**).
    1. Nginx proxy port is set to 3000. If your Node.js app listen port is not 3000, change nginx config file(**/etc/nginx/conf.d/default.conf**).
    1. Add run command(ex: node /var/local_shared/app.js) to **/root/src/cmd.sh** for node.js application auto start.
    1. If necessary, connect to the container and make additional settings.
        - Environment variables, project config, and etc...
        - Or [jwilder/nginx-proxy](https://hub.docker.com/r/jwilder/nginx-proxy/)

1. Contents of dockerfile:
    - Creates from the centos:6.10 Docker image.
    - Install Nginx(ver 1.10)
    - Install Node.js(ver 8.12)
    - Set default.conf
        - Set proxy to 3000
    - Set **EXPOSE**
        - 80 443 3000
    - Add **ENV**
        - 'VIRTUAL_HOST'. It use 'nginx-proxy' container.
            - [jwilder/nginx-proxy](https://hub.docker.com/r/jwilder/nginx-proxy/)
    - Set **VOLUME**
        - '/var/local_shared'
    - Set **CMD**
        - run script to start httpd at container is start or restart.
