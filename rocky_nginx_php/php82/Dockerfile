# Set baseImage and metadata
FROM rockylinux:9.2
LABEL Name=RockyLinux-Nginx-PHP82 \
    Version=1.0.0 \
    Description=" \
Rocky Linux 9.2 \
Nginx 1.20.1 \
PHP 8.2.12" \
    BaseImage=rockylinux:9.2

# Copy cop_files and set WORKDIR
COPY ./copy_files /root/src
WORKDIR /root/src

## Install packages
RUN dnf -y update && \
    dnf -y install epel-release && \
    dnf -y install nginx && \ 
    dnf -y install http://rpms.remirepo.net/enterprise/remi-release-9.rpm && \
    dnf -y install dnf-utils && \
    dnf module reset php && \
    dnf -y module install php:remi-8.2 && \
    dnf -y install php php-intl php-cli php-common php-mbstring \
        php-mcrypt php-gd php-mysql php-mysqlnd php-ldap php-xml \
        php-curl php-fileinfo php-gettext php-zip php-grpc php-json \
        php-dba php-dbg php-devel php-embedded php-enchant php-gmp \
        php-odbc php-pdo php-opcache php-pear php-pgsql php-process \
        php-snmp php-soap && \
    mkdir -p /var/run/php-fpm && \
    mkdir -p /var/www/approot && \
    cp /root/src/www.conf /etc/php-fpm.d/www.conf && \
    cp /root/src/php.ini /etc/php.ini && \
    cp /root/src/nginx.conf /etc/nginx/nginx.conf
# RUN php -r "copy('https://getcomposer.org/installer', '/root/src/composer-setup.php');" && \
#     php -r "if (hash_file('sha384', '/root/src/composer-setup.php') === '8a6138e2a05a8c28539c9f0fb361159823655d7ad2deecb371b04a83966c61223adc522b0189079e3e9e277cd72b8897') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('/root/src/composer-setup.php'); } echo PHP_EOL;" && \
#     php /root/src/composer-setup.php && \
#     php -r "unlink('/root/src/composer-setup.php');" && \
#     mv /root/src/composer.phar /usr/local/bin/composer && \
#     chmod +x /usr/local/bin/composer
    

# Configure
WORKDIR /var/www/approot
EXPOSE 80 443
ENV VIRTUAL_HOST=hostname.for.docker-proxy.connect
ENV HTTPS_METHOD=noredirect
ENV TZ=Asia/Seoul
VOLUME ["/var/www/approot"]

# Set ENTRYPOINT and CMD
#ENTRYPOINT sh /root/src/entrypoint.sh
CMD sh /root/src/cmd.sh
