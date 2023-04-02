# 如何在 Node.js 中获取不带扩展名的文件名

> 原文：<https://javascript.plainenglish.io/node-js-get-file-name-without-extension-2d33f1716733?source=collection_archive---------5----------------------->

## 关于如何在 Node.js 中轻松获得不带扩展名的文件名的教程

![](img/6b3d0dd0fa9da3ae3015434a93c0a0f9.png)

要获取 Node.js 中不带扩展名的文件名，请使用来自`path`模块的`parse()`方法来获取表示路径的对象。该对象的`name`属性将包含不带扩展名的文件名。

例如:

```
const path = require('path');path.parse('index.html').name; // indexpath.parse('package.json').name; // packagepath.parse('image.png').name; // image
```

# `parse()`方法

`parse()`方法返回一个对象，其属性代表给定路径的主要部分。它返回的对象具有以下属性:

1.  `dir` -路径的目录。
2.  `root` -操作系统中最顶层的目录。
3.  `base` -路径的最后一部分。
4.  `ext` -文件的扩展名。
5.  `name` -不带扩展名的文件名。

```
path.parse('C://Code/my-website/index.html');/*
Returns:
{
  root: 'C:/',
  dir: 'C://Code/my-website',
  base: 'index.html',
  ext: '.html',
  name: 'index'
}
*/
```

如果路径不是字符串，`parse()`抛出一个`TypeError`。

```
// ❌ TypeError: Received type of number instead of string
path.parse(123).name;// ❌ TypeError: Received type of boolean instead of string
path.parse(false).name;// ❌ TypeError: Received type of URL instead of string
path.parse(new URL('https://example.com/file.txt')).name;// ✅ Received correct type of string
path.parse('index.html').name; // index
```

*最初发表于*[*codingbeautydev.com*](https://cbdev.link/b5b3c2)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。