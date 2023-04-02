# 如何在 Node.js 中获取文件的扩展名

> 原文：<https://javascript.plainenglish.io/node-js-get-file-extension-5d0e35971857?source=collection_archive---------11----------------------->

## 如何轻松获取 Node.js 中文件扩展名的教程

![](img/f8940f1d59b91d0f7658eed9aff890d7.png)

要获得 Node.js 中文件的扩展名，我们可以使用来自`path`模块的`extname()`方法。

例如:

```
const path = require('path');path.extname('style.css') // .csspath.extname('image.png') // .pngpath.extname('prettier.config.js') // .js
```

# `extname()`法

`extname()`方法返回给定路径从最后一个出现的`.`(句点)字符到路径最后部分的字符串结尾的长度。

如果路径的最后一部分没有`.`，或者路径以`.`开始，并且它是路径中唯一的`.`字符，`extname()`返回一个空字符串。

```
path.extname('index.'); // .path.extname('index'); // '' (empty string)path.extname('.index');   // '' (empty string)path.extname('.index.html'); // .html
```

如果路径不是字符串，`extname()`抛出一个`TypeError`。

```
const path = require('path');// ❌ TypeError: Received type number instead of string
path.extname(123);// ❌ TypeError: Received type boolean instead of string
path.extname(false);// ❌ TypeError: Received URL instance instead of string
path.extname(new URL('https://example.com/file.txt'));// ✅ Received type of string
path.extname('package.json'); // .json
```

*原载于*[*codingbeautydev.com*](https://cbdev.link/fd2333)

# ES13 中 11 个惊人的新 JavaScript 特性

本指南将带您快速了解 ECMAScript 13 中添加的所有最新功能。这些强大的新特性将会用更短、更富于表现力的代码来更新您的 JavaScript。

![](img/75a56482761ab63cfc081ad691d70d61.png)

[**报名**](https://cbdev.link/900477) 立即免费领取一份。