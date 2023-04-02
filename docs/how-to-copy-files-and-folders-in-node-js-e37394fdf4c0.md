# 如何复制 Node.js 中的文件和文件夹？

> 原文：<https://javascript.plainenglish.io/how-to-copy-files-and-folders-in-node-js-e37394fdf4c0?source=collection_archive---------3----------------------->

## 在 Node.js 中复制文件的多种方法

![](img/e4b2357091b082efb68403f90a3644f2.png)

Photo by [Dziana Hasanbekava](https://www.pexels.com/photo/focused-man-writing-in-account-book-at-table-7063776/)

在 Node.js 中，复制文件有多种方式。，让我们来看看可能的方法，并分析每一种方法。这是我第 44 篇中型文章。

# 1 .拷贝文件

`copyFile()`函数可以将文件直接复制到目标目录，它执行最简单的操作。

```
fs.copyFile('./data.txt', './dest/info.txt');
```

> 上述方法将文件从 src 异步复制到 dest。如果目的地已经存在，则默认情况下会被覆盖。除了任何可能的异常之外，没有任何参数传递给回调函数。Node.js 不能确保复制操作是原子的。如果在打开目标文件进行写入后发生错误，Node.js 将尝试删除目标文件。

当我们使用上述方法时，有一个缺点。如果目标目录不存在，则会引发异常，因为目标目录必须存在(该方法不会自动创建目标目录)。因此，在使用上述方法之前，用户必须验证目标目录是否确实存在？如果目标目录不存在，用户可以使用`fs.mkdir()`或`fs.mkdirSync()`创建目标目录。`copyFile()`方法不能复制目录。

# 2.readFile 和 writeFile

这样，读取源文件的内容，然后写入目标文件。如果在复制过程中必须修改源文件的内容，这种方法是合适的

这种方法的缺点与上面的`copyFile()`方法相同。`readFile()`方法用于读取源文件的内容，而`writeFile()`方法只能在现有目录中写入文件。通过使用这种方法，我们不能复制目录。使用这种方法的优点是可以在复制的同时修改内容。

# 3.createReadStream 和 createWriteStream

`readFile()`方法和`writeFile()`方法是整块运算数据。如果文件很大，上述方法会增加系统资源的压力。`createReadStream()`和`createWriteStream()`是用流的方式来操纵数据。

```
fs.createReadStream('./data.txt').pipe(fs.createWriteStream(`./info.txt`));
```

# 4.丙酸纤维素

Node.js 的 16.7.0 版本增加了新的`[fs.cp()](https://nodejs.dev/en/api/v18/fs/#fscpsrc-dest-options-callback)`方法，通过使用该方法，可以将包括子目录和文件在内的整个目录结构从 src 异步复制到 dest。方法可以复制一个文件或者一个目录。如果需要目录副本，需要将配置的`recursive`属性设置为 true。

## 复制文件

## 复制目录，包括子目录和文件。

如你所见，这个`fs.cp()`方法比上面 3 个方法好很多。

1.  不需要 dest 目录存在。如果目标目录不存在，将自动创建该目录(不考虑目录的级别)
2.  您可以完全复制整个文件夹(包括子目录)中的文件，而无需分别递归复制。

> 当您打算首先使用这种方法时，首先需要确认 Node.js 版本！

如果你想复制文件夹中的每个文件，但是你只有一个较低版本的 Node.js 怎么办？除了用于 Linux 的本机 cp 命令之外，我们还可以递归地复制一些文件，这将在下一节中介绍:

如何使用:

```
copyDir('./component', './page/home');
```

# 5.Linux 中的 cp 命令

为了执行 Linux 本地命令，我们可以使用`child_process`中的`exec`或`spawn`命令。要复制文件或目录，使用 Linux 中的 [cp 命令。](https://www.rapidtables.com/code/linux/cp.html)

# 结论

如果您使用的是最新的节点版本，您可以使用以上 5 种方法。使用节点中的 fs 模块，我已经分享了复制文件/目录的最快方法。我们彻底研究了通过 Node.js 的 fs 模块访问的异步方法。

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *

## *想扩大你的软件创业规模吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。*