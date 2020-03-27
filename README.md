# 一、安装 docker

### Linux 环境

##### deepin / ubuntu / debian
```bash
# 更新
sudo apt update

# 安装 docker
sudo apt install docker-ce

# 新建or编辑 /etc/docker/daemon.json
{
  "registry-mirrors": ["https://kv0xg7tt.mirror.aliyuncs.com"]
}

# 安装docker-compose
sudo apt install docker-compose

# 把当前“用户”加入docker组，操作完成之后最好重启一下
sudo gpasswd -a 用户 docker
```


### Windows 环境

##### win10专业版 + hyper-v
```bash
# win10 专业版 [ hyper-v ]

# 使用 PowerShell 命令行工具

# Docker for Windows

# 设置阿里云的源 https://kv0xg7tt.mirror.aliyuncs.com
```

# 二、运行 docker

```bash
# 路径 /x 【windows 上 x 代表盘符，比如 D 盘，就用 /d 表示】

# 在路径 /x 下建立 www 目录
/x/www

# 在路径 /x 下 git 【 请注意：是 http 】
git clone http://git.i-sanger.com/a/dp72dev.git

# 复制 .env 文件
cd /x/dp72dev
cp .env.example .env

# 配置编辑 /x/dp72dev/.env 文件
WORKER_DIR=/x/www
...
...

# 启动 docker 【在 /x/dp72dev 目录下，执行命令行】
docker-compose up -d

# 停止 docker 【在 /x/dp72dev 目录下，执行命令行】
docker-compose down

# 重新构建 【在 /x/dp72dev 目录下，执行命令行】
docker-compose up -d --build
```


# 附录、docker 的一些操作
```bash
# 【镜像】获取一个镜像
docker pull xxx:[tag]

# 【镜像】查看已经下载的 docker 镜像
docker images

# 【镜像】删除一个已有镜像
ocker rmi xxx:[tag]

# 【容器】查看所有容器
docker ps -a

# 【容器】查看正在运行的容器
docker ps

# 【容器】删除一个容器
docker rm xxx

# 【容器】创建一个容器[nginx]
docker run --name my_nginx_1 -p 80:80 -d nginx

# 【容器】启动一个容器
docker start my_nginx_1

# 【容器】停止一个容器
docker stop my_nginx_1

# 【容器】进入一个容器
docker exec -it my_nginx_1 sh

# 【数据卷】创建一个数据卷
docker volume create my_data_vol

# 【数据卷】查看数据卷
docker volume inspect my_data_vol

# 【命令行】进入一个正在运行的 docker 容器内部
docker exec -it lnmp_php_1 bash
docker exec -it lnmp_nginx_1 sh

# 【命令行】重启 nginx
docker exec -it lnmp_nginx_1 nginx -s reload
```


# 附录、PHP7.2.19 镜像包含的扩展
```
[PHP Modules]
bcmath、 Core、 ctype、 curl、 date、 dom
exif、 fileinfo、 filter、 ftp、 gd、 hash
iconv、 json、 libxml、 mbstring、 memcached
mongodb、 mysqli、 mysqlnd、 openssl、 pcntl
pcre、 PDO、 pdo_mysql、 pdo_sqlite、 Phar
posix、 readline、 redis、 Reflection、 session
SimpleXML、 soap、 sockets、 sodium、 SPL
sqlite3、 standard、 swoole、 tokenizer
xdebug、 xml、 xmlreader、 xmlwriter、 yaf
Zend OPcache、 zip、 zlib

[Zend Modules]
Xdebug
Zend OPcache
```
