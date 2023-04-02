# 终端中的乐趣:外壳中的 JavaScript

> 原文：<https://javascript.plainenglish.io/fun-in-the-terminal-js-in-the-shell-a650b8ea2c67?source=collection_archive---------24----------------------->

![](img/1afe8a64facc4a3afd181c2673ce140b.png)

Photo by [Marc Rentschler](https://unsplash.com/@marcrnt?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

首先，让我们问问自己:

## ***shell 和 bash 脚本有什么问题？***

嗯，理论上，没有——除了你必须学习一种新的编程语言到每一个你想自动化的操作系统上(比如假装没有别的选择可以在 Windows 上运行 bash)。

有一次我在网上看到一个评论，说 JS 开发人员总是避免学习，这就是为什么他们到处都带着 JS，我认为这很有趣，大多数时候看起来真的是这样(只是说 JS 只是我知道的语言之一，不是我最喜欢的，这就是为什么我觉得它很有趣；)).

但我们也需要说，现在大部分自动化不是由 shell 或 bash 脚本完成的，而是由 **Python** 脚本完成的， **Lua** 也被大量使用，最流行的 macOS 软件包管理器使用 **ruby，**，通常当需要创建 cron 作业时，人们使用 **PHP** 来完成。

## **那么为什么不是 JavaScript 呢？**

我认为 Node.js 发布后，我们获得使用 js 自动化任务的合适替代方案只是时间问题，现在我认为我终于找到了一个非常好的工具来使用 JS。

而对于这篇文章，我们准备用 [**zx**](https://github.com/google/zx) 来为它。

Zx 是一个 JavaScript 工具，使用 JS 作为主要的 bash 脚本语言。

要开始，我们需要安装 node JS 和 npm，之后，我们只需要运行:

```
npm i -g zx
```

安装 zx 后，我们只需用。mjs 扩展
并开始编写我们的脚本。

我们应该添加到脚本中的第一行代码是:

```
#!/usr/bin/env zx
```

默认的 shell 将是 bash，所以如果您想换成另一个 shell，只需使用$。shell = shell 路径

```
$.shell = ‘C:\Windows\WinSxS\wow64_microsoft-windows-powershell-exe_31bf3856ad364e35_10.0.19041.546_none_5163f0069562aff6/powershell’
```

让我们首先创建一个文件夹

```
let folderName = ‘myzxtutorial’
await $`mkdir ${folderName}`
```

要运行它，我们只需在 shell 中键入

```
zx filepath/filename.mjs
```

我们应该得到这样的输出:

```
$ mkdir myzxtutorial
```

现在让我们在该目录中创建两个文件:

```
await $`touch myzxtutorial/file1.txt`
```

对于第二个文件，我们不用键入文件夹/文件名，而是用 cd 命令来更改目录

```
cd('myzxtutorial')
await $`touch second_file.txt`
```

如果我们在 bash 上运行，我们应该给出这样的输出:

```
$ ←[92mtouch ←[39mmyzxtutorial/file1.txt
$ ←[92mcd ←[39mmyzxtutorial
$ ←[92mtouch ←[39msecond_file.txt
```

现在让我们做一些更复杂的事情，一个 web 请求，zx 在 fetch 库中有一个包装器，允许我们做类似 JS 的请求:

```
const resp = await fetch(‘[https://httpbin.org/ip](https://httpbin.org/ip)')
if (resp.status == 200) {
 const jsonRes = JSON.parse(JSON.stringify(await resp.json()))
 console.log(jsonRes.origin)
}
```

如果我们运行这个脚本，我们将得到如下结果:

```
$ fetch [https://httpbin.org/ip](https://httpbin.org/ip)
167.249.93.243
```

好了，现在让我们通过用户使用问题功能来获得一些输入

```
const num1 = await question(‘type a number’)
console.log(`calc is ${parseInt(num1) + 2}`)
```

如果我们运行它，结果将类似于:

```
type a number4
calc is 6
```

但是我们也可以并且应该处理文件系统和操作系统，zx 在两个库周围都有包装器，为了演示，让我们在之前创建的一个文件上写内容:

```
await fs.writeFile(‘./myzxtutorial/second_file.txt’, ‘any content’)
```

如果我们打开我们的 second_file.txt 文件中的 ***【任何内容】*** 消息应该被写入文件中。

最后，让我们使用粉笔包装为终端添加一些颜色

```
console.log(chalk.blue(3))
```

运行脚本，我们应该看到蓝色的数字 3

我希望这个简短的 zx 介绍可以让你很好地理解这个不错的工具，也激发你的好奇心去了解更多，zx 有许多其他的特性和包装器，甚至有实验性的特性供你测试，所以如果你感兴趣，我建议你仔细看看[文档](https://github.com/google/zx)。
再见！

> [额外挑战警报]

创建一个脚本，使用获取包装器向***'***[***https://httpbin.org/ip***](https://httpbin.org/ip)***'***执行请求，并使用 fs 包装器将其解析为 JSON 的响应体写入 file1.txt 文件。

*更多内容请看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*