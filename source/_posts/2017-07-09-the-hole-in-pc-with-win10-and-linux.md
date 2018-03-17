---
title: "Win10+Linux 双系统方案中的 ‘坑’"
tags:
  - win10
  - linux
  - 双系统
categories: Default
toc: false
comment: true
notag: false
date: 2017-07-09 13:08:00
thumbnail: http://upload-images.jianshu.io/upload_images/4368698-07eccbbeb3f3459a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240
---

## 第一坑：双系统时间不一致

首先科普一下 [GMT 和 UTC](http://www.cnblogs.com/tosee/p/5538007.html)

Windows 和 Linux 计算系统时间的默认方法是不同的：

* Windows 把 `BIOS 时间` 当做 `系统时间`;
* Linux 把 `BIOS 时间` 当做 `UTC 时间`，而北京是东八时区，所以系统显示的时间是 UTC+8，比正常时间快了 8 小时

解决方法有下面两种：

* 让 Linux 把 BIOS 时间 当做正常时间

```shell
sudo gedit /etc/default/rcS
# 把 UTC=yes 改为 no
```

* 让 Windows 把 BIOS 时间 当做 UTC 时间

```
// 在 cmd 中输入：
Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1
```

[其他方法](http://blog.csdn.net/misiter/article/details/7767146)


## 第二坑：Win 10 关机后 Linux 对磁盘不可写

从 win 8 开始，windows 的开机速度变得飞快，其原理就是 `关机 类似于 休眠`，关机前关掉所有程序，将下次开机时需要的数据存到硬盘上，开机时只需将硬盘中的数据读取到内存中。

这样做就有一个坑，Windows 关机后再进入 Linux 系统后，硬盘的 `非 Linux 所在分区` 表现为 `只读状态`，无法写入、删除数据。

在百度上也没找到这个问题，个人认为是 Windows 的 `关机即休眠` 原理造成的，于是我做了一个测试：

> 在 Windows 重启到 BIOS 界面时立即进入 Linux 系统，这时发现 Linux 对所有磁盘的读写已经正常了

所以这个问题可以这样解决：

* 在 Windows 完全关机的状态下再进入 Linux，这种方法每次进 Linux 系统都比较麻烦
* 在 Windows 电源选项中关掉 `快速启动`，这种方法会使得 Windows 开机变慢