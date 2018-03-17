---
title: SoftEther VPN 服务搭建（Linux 版）
tags:
  - VPN
  - SoftEther
  - Linux
categories: VPN
toc: false
comment: true
notag: false
date: 2017-05-14 12:59:29
thumbnail: http://upload-images.jianshu.io/upload_images/4368698-738d39a639d5c48c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240
---

## 工具材料

* VPS / 云服务器（本文以 `Ubuntu Server 14.04.1 LTS 64bit` 系统为例）
* SoftEther VPN Server（[官方下载](http://www.softether-download.com/cn.aspx)（被墙））
* SoftEther VPN Client（[官方下载](http://www.softether-download.com/cn.aspx)（被墙）[网盘下载](https://pan.baidu.com/s/1mhY6NkG)）
* putty（[下载地址](http://www.putty.org/)）

## 安装 SoftEther VPN Server
1.登录到 VPS

Linux / OS X 下直接在 `terminal` 中登录：
```bash
ssh username@vps_ip
```
![](http://upload-images.jianshu.io/upload_images/4368698-65a8971f26d71ab5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
Windows 下使用 `putty` 登录

2.更新一下 `apt-get` 源并安装gcc等工具
```bash
sudo apt-get update
sudo apt-get install build-essential
```

3.下载 `SoftEther VPN Server` （也可以使用 `scp` 从本地上传到云服务器）
```bash
# 32bit 执行这个
wget http://opxbtqu6c.bkt.clouddn.com/SoftEther-VPN/softether-vpnserver-v4.20-9608-rtm-2016.04.17-linux-x64-64bit.tar.gz
# 64bit 执行这个
wget http://opxbtqu6c.bkt.clouddn.com/SoftEther-VPN/softether-vpnserver-v4.20-9608-rtm-2016.04.17-linux-x64-64bit.tar.gz
```
![](http://upload-images.jianshu.io/upload_images/4368698-9a4ee5c7234a21ea.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4.使用 `tar` 解压，会产生一个 `vpnserver` 文件夹
```bash
tar xvf softether-vpnserver-v4.20-9608-rtm-2016.04.17-linux-x64-64bit.tar.gz
```
![](http://upload-images.jianshu.io/upload_images/4368698-568de4bad530e2a4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

5.进入 `vpnserver` 文件夹，然后安装
```bash
cd vpnserver
make
```
连续输3次1同意许可协议
![](http://upload-images.jianshu.io/upload_images/4368698-e9602a8974b7691f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](http://upload-images.jianshu.io/upload_images/4368698-5e3cebbfa949a5cd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 配置 SoftEther VPN Server

1.开启 `vpn` 服务
```bash
sudo /home/ubuntu/vpnserver/vpnserver start
```

2.执行以下命令，然后依次输入1、回车、回车
```bash
/home/ubuntu/vpnserver/vpncmd
```
![](http://upload-images.jianshu.io/upload_images/4368698-97b006b192194254.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](http://upload-images.jianshu.io/upload_images/4368698-a4130440cda70a40.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3.输入以下命令设置管理密码，之后按 `Ctrl+C` 退出 vpncmd
```
ServerPasswordSet
```

4.将 `vpnserver` 加入开机启动项（可选）
```bash
vi /etc/rc.local
```
按 `i` 键，将 `/home/ubuntu/vpnserver/vpnserver start` 写入文件，按下 `ESC` ，输入 `:wq` 退出

## 管理 SoftEther VPN Server

SoftEther 提供了 `图形界面` 的 `vpn server` 管理工具，目前有 `Windows` 版和 `OS X` 版（推荐 win 版，支持中文）

1.打开 VPN Server Manager ，添加新设置

![](http://upload-images.jianshu.io/upload_images/4368698-f49bf1352f334d3c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/400)

填入server端的 `ip` 和 `端口` 以及 `管理员` 的 `密码`

![](http://upload-images.jianshu.io/upload_images/4368698-de74be5b6b6b8c54.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)

2.连接server端

![](http://upload-images.jianshu.io/upload_images/4368698-4dd18fe21c8d191a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/400)

勾选远程访问

![](http://upload-images.jianshu.io/upload_images/4368698-c0446980957046a2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)

默认 VPN

![](http://upload-images.jianshu.io/upload_images/4368698-0012b56d655b0df3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)

![](http://upload-images.jianshu.io/upload_images/4368698-d25b5b955befc212.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)

如果需要开启其他平台的设备连接 VPN ，则勾选并设置秘钥

![](http://upload-images.jianshu.io/upload_images/4368698-fb01b749218ac0d7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)

禁用 VPN Azure

![](http://upload-images.jianshu.io/upload_images/4368698-3001db760593919f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)

![](http://upload-images.jianshu.io/upload_images/4368698-328d0f8bcc393bc9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)

创建用户，填入用户名、密码，验证类型选密码验证

![](http://upload-images.jianshu.io/upload_images/4368698-e01480e134e56167.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)


## 连接 SoftEther VPN Server

SoftEther 也提供了 `图形界面` 的 `SoftEther VPN Client`

1.安装 `SoftEther VPN Client` ，然后打开

![](http://upload-images.jianshu.io/upload_images/4368698-3e9fcf6fcde3a065.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)

2.添加新的连接

![](http://upload-images.jianshu.io/upload_images/4368698-020e09218b76b19a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)

使用默认的 `VPN` 作为适配器名

![](http://upload-images.jianshu.io/upload_images/4368698-57917ea02d75b49b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)

![](http://upload-images.jianshu.io/upload_images/4368698-e14faab13ca513d9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)

3.再次点击添加新的连接

![](http://upload-images.jianshu.io/upload_images/4368698-020e09218b76b19a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)

填入server端的 `ip` 和 `端口` 以及server端添加的 `用户 `的 `用户名` 和 `密码`

![](http://upload-images.jianshu.io/upload_images/4368698-46e42a2abb1fa370.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)

4.回到主界面连接即可