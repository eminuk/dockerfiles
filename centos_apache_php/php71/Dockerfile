# Set baseImage and metadata
FROM centos:6.10
LABEL Name=CentOS-Apach-PHP56 \
    Version=1.0.1 \
    Description=" \
CentOS 6.10 \
Apache 2.2 \
PHP 7.1" \
    BaseImage=centos:6.10

# Copy cop_files and set WORKDIR
COPY ./copy_files /root/src
WORKDIR /root/src

# Install packages
RUN yum -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm \
        http://rpms.remirepo.net/enterprise/remi-release-6.rpm \
        yum-utils && \
    yum-config-manager --enable remi-php71 && \
    yum -y install php php-mcrypt php-cli php-gd php-curl php-mysql php-ldap php-zip php-fileinfo \
        php-mbstring php-gettext php-xml php-fpm && \
    cp /root/src/httpd.conf /etc/httpd/conf/httpd.conf && \
    cp /root/src/php.ini /etc/php.ini

# Configure
WORKDIR /var/local_shared
EXPOSE 80 443
ENV VIRTUAL_HOST=hostname.for.docker-proxy.connect
VOLUME ["/var/local_shared"]

# Set ENTRYPOINT and CMD
#ENTRYPOINT sh /root/src/entrypoint.sh
CMD sh /root/src/cmd.sh
