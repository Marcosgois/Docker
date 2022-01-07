FROM php:7.3-apache

LABEL maintainer="Antonio Sanna <atsanna@tiscali.it>"

RUN apt-get update
RUN apt-get upgrade -y

RUN apt-get install --fix-missing -y libpq-dev
RUN apt-get install --no-install-recommends -y libpq-dev
<<<<<<< HEAD:Dockerfile
RUN apt-get install -y libxml2-dev libbz2-dev zlib1g-dev libpng-dev
=======
RUN apt-get install -y \
    sudo \
    nano \
    libxml2-dev \
    libbz2-dev \
    zlib1g-dev \
    libicu-dev \
    libpng-dev \
    libjpeg-dev \
    libmcrypt-dev \
    libreadline-dev \
    libfreetype6-dev
    
>>>>>>> af2fb75be5037113f8e390a2f42b0ad001c2041a:CodeIgniter4_Jenkins_PhPmyadmin_mariadb/Dockerfile
RUN apt-get -y install libsqlite3-dev libsqlite3-0 mariadb-client curl exif ftp
RUN docker-php-ext-install intl
RUN docker-php-ext-install mysqli pdo pdo_mysql
RUN docker-php-ext-install gd
RUN docker-php-ext-enable mysqli
RUN docker-php-ext-enable pdo
RUN docker-php-ext-enable pdo_mysql
RUN docker-php-ext-enable gd
RUN apt-get -y install --fix-missing zip unzip
RUN apt-get -y install --fix-missing git

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd

# Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
RUN composer self-update --2

ADD conf/apache.conf /etc/apache2/sites-available/000-default.conf

# LDAP INSTALLATION
RUN set -x \
    && apt-get update \
    && apt-get install -y libldap2-dev \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ \
    && docker-php-ext-install ldap \
    && apt-get purge -y --auto-remove libldap2-dev

RUN a2enmod rewrite

#ADD startScript.sh /startScript.sh
# The printf command below creates the script /startScript.sh with the following 3 lines. 
# #!/bin/bash
# mv /codeigniter4 /var/www/html
# /usr/sbin/apache2ctl -D FOREGROUND
RUN printf "#!/bin/bash\nmv /codeigniter4 /var/www/html\n/usr/sbin/apache2ctl -D FOREGROUND" > /startScript.sh
RUN chmod +x /startScript.sh

RUN cd /var/www/html

RUN composer create-project codeigniter4/appstarter codeigniter4 v4.1.5
RUN chmod -R 0777 /var/www/html/codeigniter4/writable

RUN mv codeigniter4 /

RUN apt-get clean \
    && rm -r /var/lib/apt/lists/*
    
EXPOSE 80
VOLUME ["/var/www/html", "/var/log/apache2", "/etc/apache2"]

CMD ["bash", "/startScript.sh"]

# http://code.visitanyplace.com/add-gd-library-with-jpg-support-extension-on-docker/ # Help with gd
