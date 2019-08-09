FROM centos

#MAINTAINER
MAINTAINER  liangyelyl@126.com

#version defined
ENV SWOOLE_VERSION 4.4.3
ENV PHPREDIS_VERSION 5.0.2
ENV PHPMONGODB_VERSION 1.5.5
ENV NGINX_VERSION 1.17.2
#update core
RUN yum install -y epel-release
RUN rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
RUN yum clean all
RUN yum update -y


#复制解压
#ADD nginx-1.17.2.tar.gz  /usr/local/src


#RUN cd /usr/local/src/nginx-1.17.2 \
#    && mkdir /usr/local/nginx \
#    && ./configure --prefix=/usr/local/nginx && make && make install \
#    && ln -s /usr/local/nginx/sbin/nginx /usr/local/sbin/ \
#    && nginx


#安装依赖库
RUN yum -y install gcc make pcre-devel zlib-devel tar zlib
#install libs
RUN yum install -y curl zip unzip  wget openssl-devel gcc-c++  autoconf

#install nginx 
RUN wget http://mirrors.sohu.com/nginx/nginx-${NGINX_VERSION}.tar.gz -O nginx.tar.gz \
    && mkdir -p nginx \
    && tar -xf nginx.tar.gz -C nginx --strip-components=1 \
	cd nginx\
    && rm nginx.tar.gz \ 
	&& mkdir /usr/local/nginx \
    && ./configure --prefix=/usr/local/nginx && make && make install \
    && ln -s /usr/local/nginx/sbin/nginx /usr/local/sbin/ \
    && nginx \
	&& rm -r nginx
	
#端口
EXPOSE 80


#install php
 
RUN yum install -y php72w-devel php72w-openssl php72w-gd php72w-mbstring php72w-mysqli  php72w-fpm  php72w-bcmath

# composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/bin/composer \
    && composer self-update --clean-backups

# use aliyun composer
RUN composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/



# swoole ext
RUN wget https://github.com/swoole/swoole-src/archive/v${SWOOLE_VERSION}.tar.gz -O swoole.tar.gz \
    && mkdir -p swoole \
    && tar -xf swoole.tar.gz -C swoole --strip-components=1 \
    && rm swoole.tar.gz \
    && ( \
    cd swoole \
    && phpize \
    && ./configure --enable-openssl \
    && make \
    && make install \
    ) \
    && sed -i "2i extension=swoole.so" /etc/php.ini \
    && rm -r swoole
	
#redis  ext

RUN wget http://pecl.php.net/get/redis-${PHPREDIS_VERSION}.tgz -O redis.tgz \
	&& mkdir -p phpredis \
	&& tar -xf redis.tgz -C phpredis --strip-components=1 \
	&& rm redis.tgz \
	&& ( \
    cd phpredis \
    && phpize \
    && ./configure  \
    && make \
    && make install \
    ) \
	&& sed -i "2i extension=redis.so" /etc/php.ini \
    && rm -r phpredis
	
#mongo  ext	

RUN wget https://pecl.php.net/get/mongodb-${PHPMONGODB_VERSION}.tgz -O mongodb.tgz \
	&& mkdir -p phpmongodb \
	&& tar -xf mongodb.tgz -C phpmongodb --strip-components=1 \
	&& rm mongodb.tgz \
	&& ( \
    cd phpmongodb \
    && phpize \
    && ./configure  \
    && make \
    && make install \
    ) \
	&& sed -i "2i extension=mongodb.so" /etc/php.ini \
    && rm -r phpmongodb


#redis sever


#mongo server


#mysql server

