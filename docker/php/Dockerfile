FROM centos:7.9.2009

# TimeZone
RUN cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

# Package
RUN yum -y update
RUN yum -y install vim

# Apache
RUN yum -y install httpd httpd-devel mod_ssl

# epel
RUN yum -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
# php
RUN yum -y install https://rpms.remirepo.net/enterprise/remi-release-7.rpm
RUN yum-config-manager --disable 'remi-php*'
RUN yum-config-manager --enable remi-php74
RUN yum -y install php php-devel php-fpm php-gd php-mbstring php-intl php-mysql php-pdo php-xml

# Composer
RUN yum -y install git zip unzip
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

# CakePHP4.4
WORKDIR /var/www
RUN composer create-project -n --prefer-dist cakephp/app:4.4.* html
WORKDIR /var/www/html
RUN rm -rf .gitignore
RUN rm -rf config
RUN rm -rf src
RUN rm -rf templates
RUN rm -rf tests
RUN rm -rf webroot

# Service enable
RUN systemctl enable httpd
RUN systemctl enable php-fpm

# Command
COPY startup.sh /startup.sh
ENTRYPOINT ["/startup.sh"]