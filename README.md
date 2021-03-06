[TOC]

## 分支说明

* master: 包含PHP/Nginx/MySQL/Redis
* mailhog: 包含PHP/Nginx/MySQL/Redis/Mailhog，邮件服务器



## 目录说明

- data：存放redis，mysql数据

- doc：暂无作用

- etc：存放各个服务的配置

  > 其中最重要的是site目录，所有站点的nginx配置全部存放在该目录下

- log：存放各个服务的日志



## 文件说明

- .env：管理各个服务的版本和基本配置

  > 其中有个关键配置项WORKSPACE_DIR，用于设置nginx服务器的工作目录

## 准备工作

1. `git clone git@github.com:hdlovefork/DRIMP.git`
2. `cd DRIMP`
3. 修改.env文件，将WORKSPACE_DIR设置成你所有项目所在目录，比如你有个myblog的项目在`/Users/dean/Workspace/myblog`下，那么`WORKSPACE_DIR=/Users/dean/Workspace`
4. `docker-compose up -d`安装各个服务

## 新增网站

​   本示例演示如何添加一个Laravel的myblog站点，域名为myblog.cn，假设myblog项目位于WORKSPACE_DIR/myblog

1. 将`etc/site/default.laravel.conf` 复制一份另取个名称如myblog.conf

   `cp etc/site/default.laravel.conf etc/site/myblog.conf`

2. 修改myblog.conf文件

   - 修改第5行server_name项为你自己的域名`myblog.cn`
   - 修改第10行root项为`/var/www/html/myblog/public`

3. 修改/etc/hosts文件添加如下配置

   > 127.0.0.1 myblog.cn

4. 重启服务
   `cd DRIMP`

   `docker-compose restart`

5. 好了，现在尝试在浏览器打开[myblog.cn](http://myblog.cn)



## 进入PHP服务执行命令

PHP服务中默认已经安装各种PHP扩展，Composer，Nodejs等，进入PHP服务的方法：

`docker-compose exec php bash`执行该命令后会进入你的WORKSAPCE_DIR目录，然后`cd myblog`项目中可以执行`composer install` `npm install` `php artisan migrate`等命令



## 导入导出数据库

### 导出

1. `cd DRIMP`
2. 这里将myblog数据库备份到`~/database/myblog.sql`位置，命令：​	`docker-compose exec mysql mysqldump -uroot -proot myblog > ~/database/myblog.sql`

### 导入

1. `cd DRIMP`
2. 恢复`myblog`数据库，命令：`docker-compose exec mysql mysql -uroot -proot myblog < ~/database/myblog.sql`