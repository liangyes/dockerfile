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




#安装依赖库
RUN yum -y install gcc make pcre-devel zlib-devel tar zlib
#install libs
RUN yum install -y curl zip unzip  wget openssl-devel gcc-c++  autoconf

#install nginx 
RUN wget http://mirrors.sohu.com/nginx/nginx-${NGINX_VERSION}.tar.gz -O nginx.tar.gz \
    && mkdir -p nginx \
    && tar -xf nginx.tar.gz -C nginx --strip-components=1 \
	&& rm nginx.tar.gz \ 
	&& ( \
	cd nginx \
	&& mkdir /usr/local/nginx \
    && ./configure --prefix=/usr/local/nginx && make && make install \
    && ln -s /usr/local/nginx/sbin/nginx /usr/local/sbin/ \
    && nginx \
	) \
	&& rm -r nginx
	
#端口
EXPOSE 80



#install php

#laravel php72w-bcmath   php72w-xmlrpc  php72w-xml
RUN yum install -y php72w-devel php72w-openssl php72w-gd php72w-mbstring php72w-mysqli  php72w-fpm  php72w-bcmath    php72w-xmlrpc  php72w-xml