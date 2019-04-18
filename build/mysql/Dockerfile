##############################################################
# 基于官方镜像 mysql:$VERSION 制作
# 暴露端口：3306
# 数据文件地址：/var/lib/mysql
##############################################################

ARG VERSION
FROM mysql:$VERSION

LABEL maintainer="whoru.S.Q <whoru@sqiang.net>"
LABEL version="1.0"

# 写权限
RUN usermod -u 1000 mysql \
	&& chown mysql.mysql /var/run/mysqld/

