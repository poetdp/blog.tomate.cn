---
title: "克隆 Github 项目的非 master 分支"
tags:
  - clone
  - branch
  - github
categories: Git
toc: false
comment: true
notag: false
date: 2017-05-01 16:37:33
thumbnail: http://upload-images.jianshu.io/upload_images/4368698-d6eb15f8d98264da.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240
---

### Step.1 Clone Repo

切换路径
```bash
$ cd path
```

克隆仓库
```bash
$ git clone git@github.com:username/Repo.git
```

### Step.2 Checkout Branch

进入目录
```bash
$ cd RepoPath
```

创建并跟踪分支
```bash
$ git checkout -b branchName origin/branchName
```