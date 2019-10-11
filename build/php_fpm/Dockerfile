##############################################################
# 基于官方镜像 php:$VERSION-fpm 制作
# 安装的 PHP 扩展：
#   - pdo_mysql、mysqli
#   - gd
#   - redis
#   - xdebug
#   - iconv
#   - mcrypt
#   - pcntl
# PHP 配置文件：
#   - /usr/local/etc/php/php.ini
# PHP-fpm 配置文件：
#   -
# WEB 根目录：
#   - /var/www/html
##############################################################

ARG VERSION
FROM php:$VERSION-fpm

LABEL maintainer="whoru.S.Q <whoru@sqiang.net>"
LABEL version="1.0"

# 修改软件更新源
COPY ./source.list /etc/apt/sources.list

# 添加扩展源码文件
COPY ./ext/*.tar.gz /tmp/

# 安装扩展、配置服务
RUN apt-get update \
    # 安装扩展依赖包
    && apt-get install -y wget \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
    #################### 安装核心扩展（PHP 源码已包含） ####################
    # iconv、mcrypt、zip、gd、pdo_mysql、mysqli、pcntl
    && docker-php-ext-install -j$(nproc) iconv mcrypt zip pdo_mysql mysqli pcntl \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd  \
    #################### 通过源码包编译安装其它扩展 ####################
    # 【redis】
    && mkdir -p /tmp/redis \
    && tar -xf /tmp/redis.tar.gz -C /tmp/redis --strip-components=1 \
    && docker-php-ext-configure /tmp/redis --with-php-config=/usr/local/bin/php-config \
    && docker-php-ext-install /tmp/redis \
    # 【xdebug】
    && mkdir -p /tmp/xdebug \
    && tar -xf /tmp/xdebug.tar.gz -C /tmp/xdebug --strip-components=1 \
    && docker-php-ext-configure /tmp/xdebug --enable-xdebug \
    && docker-php-ext-install /tmp/xdebug \
    #################### 更改 web 根目录属主、属组 ####################
    # 如果发生权限问题，可添加此处修改
    # 运行时用户可通过 phinfo() 中查看 APACHE_RUN_USER 获取
    #usermod -u 1000 www-data && usermod -G staff www-data
    #&& chown www-data:www-data /var/www/html \
    #################### 清理安装过程产生的垃圾文件 ####################
    && apt-get clean \
    && apt-get autoclean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
