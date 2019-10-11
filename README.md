
一个基于 Docker 的 LNMP 环境
---

> 这是一个基于 Dokcer 的 LNMP（Nginx + PHP with FPM + MySQL） 环境，借助 Docker compose 进行编译、管理，可用于本地开发及线上部署。
>
> 因为 Docker 的限制，推荐服务器系统使用 CentOS7+、Ubuntu16.04 Server +，关于 Dokcer 的安装、设置，详见 [https://github.com/whorusq/docker-learning](https://github.com/whorusq/learning-docker)

### 1. 目录结构

```
.
├── README.md
├── build
│   ├── mysql
│   │   └── Dockerfile
│   ├── nginx
│   │   └── Dockerfile
│   └── php_fpm
│       ├── Dockerfile
│       ├── ext
│       │   ├── READEME.md
│       │   ├── redis.tar.gz
│       │   └── xdebug.tar.gz
│       └── source.list
├── conf
│   ├── mysql
│   ├── nginx
│   │   ├── cert
│   │   ├── nginx.conf
│   │   ├── rewrite
│   │   └── vhosts
│   │       ├── README.md
│   │       └── www.conf
│   └── php_fpm
│       ├── php.ini
│       └── zz-docker.conf
├── data
├── docker-compose.yml
├── log
│   ├── mysql
│   ├── nginx
│   └── php_fpm
└── www
    ├── README.md
    ├── index.html
    └── index.php
```

### 2. 使用

- 克隆或下载源码

	```bash
	➜  git clone https://github.com/whorusq/lnmp-docker.git lnmp
	```

- 替换 www 目录

	```bash
	➜  cd lnmp
	➜  mv www www_bak
	➜  ln -s /home/user1/www www
	```

- 初始化启动

	```bash
	# 初始化过程包括：构建各服务对应的镜像、基于镜像启动容器并建立关联，数据库初始化等
	➜  docker-compose up
	```

	> 如果整个过程出现 error ，初始化将终止，可针对错误信息进行调整。
	>
	> 正常启动后，目录下自动生成（如果不存在）
	>
	> - ./data MySQL 数据文件
	> - ./log 所有服务的日志文件

	```bash
	➜  cd lnmp

	# 后台启动
	➜  docker-compose up -d

	# 查看容器运行情况
	➜  docker-compose ps

	# 停止服务
	➜  docker-compose stop

	# 停止服务，并删除容器
	➜  docker-compose down
	```

### 3. 切换版本

打开 `docker-compose.yml` 文件，修改 `VERSION` 和 `image` 后面的版本号，二者保持一致。

重启

```
docker-compose down
docker-compose up
```