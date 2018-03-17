---
title: "git 使用 http(s) 协议时该如何保存用户名和密码"
tags:
  - git
  - https
  - 密码
categories: Git
toc: false
comment: true
notag: false
date: 2017-05-30 17:15:25
thumbnail: http://upload-images.jianshu.io/upload_images/4368698-3aa8df7a50bff841.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240
---

git 使用 http(s) 方式每次都要输入密码，下面有几种方法可以解决输入密码的困扰又能享受https带来的极速

* 暂时记住密码（默认15分钟）：

```bash
git config --global credential.helper cache

# 如果想自己设置时间，可以这样做：
git config credential.helper 'cache --timeout=3600'
# 这样就设置一个小时之后失效
```

* 长期存储密码：

```bash
git config --global credential.helper store
```

* 在远程地址中加上密码（推荐）

```bash
git remote add origin http://username:password@github.com/username/repo.git
```

修改已有仓库的地址可以这样做

```bash
git remote rm origin
git remote add origin http://username:password@github.com/username/repo.git
```