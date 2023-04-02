# 作为开发人员，我每天使用的 12 个终端命令

> 原文：<https://javascript.plainenglish.io/12-terminal-commands-i-use-every-day-as-a-developer-4a38135ab305?source=collection_archive---------5----------------------->

## 作为软件开发人员如何有效地使用计算机终端

![](img/d62c769d87d3589619b8b84fc0db8ea0.png)

Photo by [Ryland Dean](https://unsplash.com/@ryland_dean?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/developer?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

编写计算机程序是一回事，而成为一名高效的开发人员并以最佳方式使用计算机来简化您的开发工作流程则是另一回事。今天，如果任何人需要成为一名优秀的开发人员，他必须知道如何有效地使用计算机终端，因为它为他们节省了大量的开发时间。

从为博客文章下载目录结构的图像，到将文件从一个目录移动到另一个目录，从您的计算机向服务器传输文件，以及维护服务器，今天，一切都是通过命令行进行的。因此，了解这些终端命令至关重要。

这篇文章涵盖了 12 个顶级的终端/ Linux 命令，这些命令可以帮助技术爱好者在命令行界面的帮助下更好地浏览计算机资源。

这篇文章中的命令可以在 Linux 和 Mac 操作系统中运行。

# 1.树

你有没有想过把文件夹的目录结构做成树状布局？那你很幸运！这个命令将帮助您实现这一目标。

你需要在 macOS 上安装它。它已经在 Linux 中可用。

```
brew install tree
```

转到工作目录，在终端中键入以下命令

```
 tree 
```

# 2.男人

如果您想从下面的列表中了解有关终端命令本身的任何信息，请使用 man 命令从您终端的开发人员那里获得该命令的官方文档。

```
man ls
```

# 3.限位开关（Limit Switch）

该命令帮助您列出目录中的内容。如果您也想查看目录中的隐藏文件，请使用附加的-a 参数。

```
ls ls -a
```

# 4.激光唱片

命令允许您更改当前工作的目录。

```
cd [ Directory Name ]cd Desktop
```

# 5.触控

使用 touch 命令在工作目录中创建新文件。

```
 touch [ filename ] touch index.js
```

# 6.平均变化

将文件从一个目录移到另一个目录。这是迄今为止我在日常工作中使用的最实用的命令。

**语法:mv [文件-移动-从] [文件-移动-到]**

```
 mv ~/Downloads/file.txt ~/Documents/Work/file.txt
```

# 7.丙酸纤维素

命令允许您将文件从一个目录复制到另一个目录。

**语法:cp [文件源][文件目的]**

将文件 1 和文件 2 的内容复制到一个新文件中。

```
touch new.txtcp file-1.txt file-2.txt new.txt
```

# 8.可做文件内的字符串查找

它在终端中也称为搜索命令。它搜索一个文件并打印所有匹配给定模式的行。

**语法:grep[模式][文件名]**

```
touch index.jsecho 'console.log('hello world')' >> index.jsgrep console index.js 
```

# 9.顶端

借助这个终端命令，在终端中查看系统的状态。它包括 CPU 利用率、磁盘存储信息、软件程序的内存。

```
 top
```

# 10.猫

对于数据工程师来说，cat 命令是最方便的命令。数据分析师使用它来创建文件、查看文件内容、将两个或更多文件合并成一个文件，甚至向文件中添加数据。是的，您可以用这个命令混合两个或多个 excel 或 number 文件。

将目录中所有文件的内容合并到一个文件中。

```
cat *.txt >> ~/Desktop/combined.txt
```

将文件 1 的内容附加到文件 2 的内容的末尾。

```
cat file-1 >> file-2
```

使用 touch 命令创建文件，使用 echo 命令添加编程语句。

```
touch index.jsecho 'console.log('hello world')' >> index.js
```

# 11.显示当前工作目录

开发人员可以使用该命令查看系统中当前的公共工作目录。意思是打印工作目录。

```
 pwd 
```

# 12.lscpu / sysctl

使用此命令查看 CPU 的内容。它包括寻找系统中的核心，它的效率，以及其他与计算机 CPU 性能相关的事情。

lscpu 是一个 Linux 命令。在 mac OS 中，它的替代品是 sysctl。

```
 lscpu 
```

在 Mac OS 上获取电脑中的内核数量。

```
sysctl -a | grep machdep.cpu.core_count
```

# 结论

以上是可以用来加速开发过程的 12 个顶级终端命令。人们也可以在编程语言中使用它来创建自己的命令行界面应用程序。但是它的范围超出了这篇文章的内容。我会把它留到将来某一天。

这个帖子到此为止。感谢您阅读我的帖子，并走了这么远。

如果你喜欢这篇文章，你也可以看看我的其他文章。

[](/10-engineering-blogs-i-read-to-stay-up-to-date-with-technology-trends-faa006460fd9) [## 我阅读的 10 个工程博客，以跟上技术趋势

### 2022 年及以后的顶级工程博客。

javascript.plainenglish.io](/10-engineering-blogs-i-read-to-stay-up-to-date-with-technology-trends-faa006460fd9) [](/7-advanced-javascript-techniques-every-developer-should-know-by-now-including-code-4572d5d7a060) [## 每个开发人员现在都应该知道的 7 种高级 JavaScript 技术(包括代码)

### 用这篇文章测试你的 JavaScript 知识。

javascript.plainenglish.io](/7-advanced-javascript-techniques-every-developer-should-know-by-now-including-code-4572d5d7a060) [](/7-google-projects-that-have-helped-developers-save-tons-of-time-fa8a72d9044c) [## 帮助开发者节省大量时间的 7 个谷歌项目

### 谷歌如何帮助开发人员创建令人惊叹的应用程序。

javascript.plainenglish.io](/7-google-projects-that-have-helped-developers-save-tons-of-time-fa8a72d9044c) 

你觉得这篇文章有用吗？我是否遗漏了一些您在日常工作中使用的命令？请在评论区告诉我。我很想知道你对此的看法。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。***