# Set baseImage and metadata
FROM rockylinux:9.2
LABEL Name=RockyLinux-Nginx-PHP83 \
    Version=1.0.0 \
    Description=" \
Rocky Linux 9.2 \
Nginx 1.20.1 \
PHP 8.3.12" \
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
    dnf -y module install php:remi-8.3 && \
    dnf -y install php php-{fpm,intl,cli,common,mbstring,gd,mysql,ldap,xml,curl,zip,grpc,dba,enchant,gmp,odbc,opcache,pgsql,snmp,soap,imap,imagick,libxml,devel} && \
    mkdir -p /var/run/php-fpm && \
    mkdir -p /var/www/approot && \
    cp /root/src/www.conf /etc/php-fpm.d/www.conf && \
    cp /root/src/php.ini /etc/php.ini && \
    cp /root/src/nginx.conf /etc/nginx/nginx.conf
RUN curl -sS https://getcomposer.org/installer -o /tmp/composer-setup.php && \
    HASH=`curl -sS https://composer.github.io/installer.sig` && \
    php -r "if (hash_file('SHA384', '/tmp/composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
    php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer 
RUN curl -sS https://xdebug.org/files/xdebug-3.3.1.tgz -o /root/src/xdebug-3.3.1.tgz && \
    tar -xvzf /root/src/xdebug-3.3.1.tgz -C /root/src  && \
    cd /root/src/xdebug-3.3.1  && \
    phpize && ./configure && make && \
    cp modules/xdebug.so /usr/lib64/php/modules/ && \
    echo -e "[Xdebug]\nzend_extension = xdebug\nxdebug.mode=debug\nxdebug.client_host = \"host.docker.internal\"\n\n;xdebug.start_with_request=yes\n\nxdebug.start_with_request=trigger\nxdebug.idekey=xdebug-idkey\n\n;xdebug.log=/var/log/xdebug/xdebug.log" > /etc/php.d/99-xdebug.ini && \
    cd /root/src

# Configure
WORKDIR /var/www/approot
EXPOSE 80 443 8080
ENV VIRTUAL_HOST=hostname.for.docker-proxy.connect
ENV HTTPS_METHOD=noredirect
ENV TZ=Asia/Seoul
VOLUME ["/var/www/approot"]

# Set ENTRYPOINT and CMD
#ENTRYPOINT sh /root/src/entrypoint.sh
CMD sh /root/src/cmd.sh
