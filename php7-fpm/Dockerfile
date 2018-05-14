FROM php:7.0-fpm

MAINTAINER Damien QUEMARD <damien.quemard@gmail.com>

#Tools
RUN apt-get update
RUN apt-get install --yes --force-yes cron g++ gettext libicu-dev openssl libc-client-dev libkrb5-dev libxml2-dev libfreetype6-dev libgd-dev libmcrypt-dev bzip2 libbz2-dev libtidy-dev libcurl4-openssl-dev libz-dev libmemcached-dev libxslt-dev
RUN apt-get install -y \
        wget \
        vim \
        nano \
        git \
		unzip \
		curl

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- \
        --install-dir=/usr/local/bin \
        --filename=composer

# Timezone Configuration
ENV TZ=Europe/Paris
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# wkhtmltopdf
RUN apt-get install -y libxrender1 libfontconfig libxtst6 xz-utils xvfb
RUN curl "https://downloads.wkhtmltopdf.org/0.12/0.12.4/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz" -L -o "wkhtmltopdf.tar.xz"
RUN tar Jxvf wkhtmltopdf.tar.xz
RUN mv wkhtmltox/bin/wkhtmltopdf /usr/bin/wkhtmltopdf
RUN mv wkhtmltox/bin/wkhtmltoimage /usr/bin/wkhtmltoimage

# LDAP
RUN apt-get install libldap2-dev -y
RUN docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/
RUN docker-php-ext-install ldap

# NodeJS
RUN curl -o /usr/local/bin/n https://raw.githubusercontent.com/visionmedia/n/master/bin/n
RUN chmod +x /usr/local/bin/n
RUN n stable
RUN apt-get install -y nodejs npm
RUN npm install -g less
RUN npm install -g uglify-js
RUN npm install -g uglifycss@0.0.27


# PHP Configuration
RUN docker-php-ext-install opcache
RUN docker-php-ext-install bcmath
RUN docker-php-ext-install bz2
RUN docker-php-ext-install calendar
RUN docker-php-ext-install dba
RUN docker-php-ext-install exif
RUN docker-php-ext-configure gd --with-freetype-dir=/usr --with-jpeg-dir=/usr
RUN docker-php-ext-install gd
RUN docker-php-ext-install gettext
RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl
RUN docker-php-ext-install imap
RUN docker-php-ext-install intl
RUN apt-get install -y libmcrypt-dev
RUN docker-php-ext-install mcrypt
#RUN docker-php-ext-install pdo
RUN docker-php-ext-install pdo_mysql
#RUN docker-php-ext-install mysql
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install soap
RUN docker-php-ext-install tidy
RUN docker-php-ext-install xmlrpc
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install xsl
RUN docker-php-ext-install zip
#RUN yes '' | pecl install -f apc
RUN docker-php-ext-configure hash --with-mhash
RUN docker-php-ext-enable opcache
# Poppler-utils (pdftotext)
RUN apt-get install poppler-utils -y

#PHP.ini configuration
COPY php.ini /usr/local/etc/php/conf.d/php.ini

# Mac User
# RUN usermod -u 501 www-data

# Linux User
# RUN usermod -u 1000 www-data

RUN useradd -ms /bin/bash docker
USER docker

WORKDIR /var/www/workspace

