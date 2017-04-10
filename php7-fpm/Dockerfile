# See https://github.com/docker-library/php/blob/4677ca134fe48d20c820a19becb99198824d78e3/7.0/fpm/Dockerfile
FROM php:7.0-fpm

MAINTAINER Maxence POUTORD <maxence.poutord@gmail.com>



RUN mv /etc/apt/sources.list /etc/apt/sources.list.old
RUN echo "deb http://mirrors.163.com/debian/ jessie main non-free contrib" >> /etc/apt/sources.list
RUN echo "deb http://mirrors.163.com/debian/ jessie-updates main non-free contrib" >> /etc/apt/sources.list

RUN echo "deb http://mirrors.163.com/debian/ jessie-backports main non-free contrib" >> /etc/apt/sources.list
RUN echo "deb-src http://mirrors.163.com/debian/ jessie main non-free contrib" >> /etc/apt/sources.list
RUN echo "deb-src http://mirrors.163.com/debian/ jessie-updates main non-free contrib" >> /etc/apt/sources.list
RUN echo "deb-src http://mirrors.163.com/debian/ jessie-backports main non-free contrib" >> /etc/apt/sources.list
RUN echo "deb http://mirrors.163.com/debian-security/ jessie/updates main non-free contrib" >> /etc/apt/sources.list
RUN echo "deb-src http://mirrors.163.com/debian-security/ jessie/updates main non-free contrib" >> /etc/apt/sources.list



RUN apt-get update && apt-get install -y \
    git \
    unzip

RUN apt-get install -y build-essential

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

RUN composer config -g repo.packagist composer https://packagist.phpcomposer.com

RUN mkdir -p /usr/local/bin

RUN curl -LsS https://symfony.com/installer -o /usr/local/bin/symfony

RUN chmod a+x /usr/local/bin/symfony

# Set timezone
RUN rm /etc/localtime
RUN ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN "date"

# Type docker-php-ext-install to see available extensions
RUN docker-php-ext-install pdo pdo_mysql
RUN docker-php-ext-install gd

RUN docker-php-ext-install -j$(nproc) mysqli

# RUN apt-cache search zlib
RUN apt-get install zlib1g
RUN apt-get install zlib1g-dev
RUN docker-php-ext-install -j$(nproc) zip
RUN docker-php-ext-install -j$(nproc) bcmath
RUN pecl install igbinary

RUN apt-get install wget -y
RUN mkdir -p /tmp/rediscompile  && cd /tmp/rediscompile  && wget https://github.com/phpredis/phpredis/archive/3.1.2.zip  && unzip 3.1.2.zip  && docker-php-ext-configure /tmp/rediscompile/phpredis-3.1.2/ --enable-redis-igbinary  && docker-php-ext-install /tmp/rediscompile/phpredis-3.1.2/ && rm -r /tmp/rediscompile

RUN apt-get install nano -y

RUN echo "extension=igbinary.so" >> /usr/local/etc/php/conf.d/docker-php-ext-igbinary.ini



RUN echo 'alias sf="php app/console"' >> ~/.bashrc
RUN echo 'alias sf3="php bin/console"' >> ~/.bashrc

WORKDIR /var/www/symfony
