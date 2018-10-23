# Set baseImage and metadata
FROM centos:6.10
LABEL Name=CentOS-Nginx-node \
    Version=1.0.1 \
    Description=" \
CentOS 6.10 \
Nginx 1.10 \
Node.js 8.12" \
    BaseImage=centos:6.10

# Copy cop_files and set WORKDIR
COPY ./copy_files /root/src
WORKDIR /root/src

# Install packages
RUN yum -y install epel-release && \
    yum -y install nginx && \
    curl --silent --location https://rpm.nodesource.com/setup_8.x | bash - && \
    yum -y install nodejs && \
    cp /root/src/default.conf /etc/nginx/conf.d/default.conf

# Configure
WORKDIR /var/local_shared
EXPOSE 80 443 3000
ENV VIRTUAL_HOST=hostname.for.docker-proxy.connect
VOLUME ["/var/local_shared"]

# Set ENTRYPOINT and CMD
#ENTRYPOINT sh /root/src/entrypoint.sh
CMD sh /root/src/cmd.sh