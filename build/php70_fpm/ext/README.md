下载 PHP 扩展源码文件

> 插件版本需保证对当前 PHP 版本的支持，并优先选择最新稳定版。

- 扩展：redis

	```bash
	wget -c https://github.com/phpredis/phpredis/archive/3.1.6.tar.gz
	mv 3.1.6.tar.gz redis.tar.gz
	```

- 扩展：xdebug

	```bash
	wget -c https://github.com/xdebug/xdebug/archive/2.6.0.tar.gz
	mv 2.6.0.tar.gz xdebug.tar.gz
	```

- 扩展：gearman

	```bash
    wget -c https://launchpad.net/gearmand/1.2/1.1.12/+download/gearmand-1.1.12.tar.gz
	wget -c https://github.com/gearman/gearmand/releases/download/1.1.18/gearmand-1.1.18.tar.gz
	mv gearmand-1.1.18.tar.gz gearmand.tar.gz

    wget -c http://pecl.php.net/get/gearman-1.1.1.tgz
	wget -c https://github.com/wcgallego/pecl-gearman/archive/gearman-2.0.3.tar.gz
	mv gearman-2.0.3.tar.gz gearman.tar.gz

	wget -c http://nchc.dl.sourceforge.net/project/libuuid/libuuid-1.0.3.tar.gz
	mv libuuid-1.0.3.tar.gz libuuid.tar.gz
	```
