# Set baseImage and metadata
FROM centos:8
LABEL Name=CentOS-Apach-PHP74 \
    Version=1.0.1 \
    Description=" \
CentOS 8 \
Apache 2.4 \
PHP 7.4" \
    BaseImage=centos:8

# Copy cop_files and set WORKDIR
COPY ./copy_files /root/src
WORKDIR /root/src

## Install packages
RUN dnf -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm && \
    dnf -y install https://rpms.remirepo.net/enterprise/remi-release-8.rpm && \
    dnf -y module enable php:remi-7.4 && \
    dnf -y install php php-intl php-cli php-common \
        php-mcrypt php-gd php-mysql php-ldap php-zip \
        php-curl php-fileinfo php-gettext && \
    mkdir -p /var/run/php-fpm && \
    cp /root/src/httpd.conf /etc/httpd/conf/httpd.conf && \
    cp /root/src/php.ini /etc/php.ini
    

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
