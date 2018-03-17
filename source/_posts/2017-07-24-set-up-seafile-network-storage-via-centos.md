---
title: "基于 CentOS 搭建 Seafile 个人网盘"
tags:
  - CentOS
  - Seafile
  - 网盘
categories: 折腾
toc: false
comment: true
notag: false
date: 2017-07-24 16:04:58
thumbnail:
---

## 准备域名

- 域名注册
- 域名解析

域名购买完成后, 需要将域名解析到云主机上，通 `ping` 命令检查域名是否生效，如：

```
ping www.yourdomain.com
```

如果 `ping` 命令返回的信息中含有你设置的解析的 IP 地址，说明解析成功。

> 注意替换下面命令中的 www.yourdomain.com 为您自己的注册的域名

## 安装 Seafile

**安装依赖环境**

使用 yum 安装 Python 及 MySQL：

```
yum install python python-setuptools python-imaging python-ldap python-memcached MySQL-python mariadb mariadb-server
```

启动 MariaDB 服务：

```
sudo systemctl start mariadb.service
sudo systemctl enable mariadb.service
```

配置 MySQL：

```
/usr/bin/mysql_secure_installation
```

配置过程输入参数如截图所示，其中 `New password` 和 `Re-enter new password` 字段都为你自己设置的密码 `yourmysqlpassword`，其他字段一路回车使用默认值：

![](http://upload-images.jianshu.io/upload_images/4368698-3ad5bb73b5da05f0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**安装 Seafile**

下载 Seafile 安装包：

```
wget http://seafile-downloads.oss-cn-shanghai.aliyuncs.com/seafile-server_6.1.1_x86-64.tar.gz
```

解压 Seafile 安装包：

```
tar -zxvf seafile-server_6.1.1_x86-64.tar.gz
```

安装 Seafile 安装包：

```
sudo mkdir -p /opt/seafile/installed
sudo mv seafile-server_6.1.1_x86-64.tar.gz /opt/seafile/installed
sudo mv seafile-server-6.1.1/ /opt/seafile
cd /opt/seafile/seafile-server-6.1.1
sudo ./setup-seafile-mysql.sh
```

执行过程输入参数如截图所示，[server name] 字段输入 `Seafile`，[ This server's ip or domain ] 字段输入教程第一步申请的域名，[ 1 or 2 ] 字段选择 1，mysql 的 [ root password ] 字段输入你自己设置的密码 `yourmysqlpassword`，其他字段一路回车使用默认值：

![](http://upload-images.jianshu.io/upload_images/4368698-bafb4a1b2054c922.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**启动 Seafile 及修改防火墙规则**

启动 Seafile

```
sudo ./seafile.sh start
sudo ./seahub.sh start
```

执行过程输入参数如截图所示，其中 [ admin email ] 设置为您登录网盘的 `邮箱帐号`，[ admin password ] 和 [ admin password again ] 设置为登录网盘的 `密码` ：

![](http://upload-images.jianshu.io/upload_images/4368698-e04142f8a9cfb762.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

修改防火墙规则（可选）

```
sudo firewall-cmd --zone=public --permanent --add-port=8082/tcp
sudo firewall-cmd --zone=public --permanent --add-port=8000/tcp
sudo firewall-cmd --reload
```

大功告成！你的 Seafile 已经部署完成，登录的帐号密码为您启动 Seafile 步骤中设置的邮箱和密码。

- 可以通过 Ip 访问网盘：http://<你的ip>:8000
- 也可以通过域名访问网盘：如 http://www.yourdomain.com:8000 ，其中 www.yourdomain.com 替换为您注册的域名