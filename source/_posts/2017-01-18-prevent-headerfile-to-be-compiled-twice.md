---
title: "#ifndef 防止头文件被多次编译"
date: 2017-01-18 19:58:28
tags:
- c
- c++
- learn
categories: C/C++
thumbnail:
toc: false
comment: true
notag: false
---

在 C/C++ 工程中，某个头文件可能会被多个文件包含，编译时就会报错，要想这个头文件在编译时只被包含一次，有如下办法：

- 在 .h 头部加上

```c
#pragma once
```
从`Visual Studio 2003`开始就支持这个 directive，如果是 Visual Studio 6.0 就不支持了

- 条件编译

```c
#ifndef _HEADFILE_H_
#define _HEADFILE_H_

//在这里写你的头文件内容

#endif
```
`_HEADFILE_H_` 为宏名，用以区分不同的条件编译程序段
