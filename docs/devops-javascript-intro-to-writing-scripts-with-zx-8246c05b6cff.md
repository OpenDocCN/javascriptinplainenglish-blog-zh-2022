# devo PS JavaScript——用 zx 编写脚本简介

> 原文：<https://javascript.plainenglish.io/devops-javascript-intro-to-writing-scripts-with-zx-8246c05b6cff?source=collection_archive---------20----------------------->

## 通过使用 zx.js 编写脚本成为一名 JavaScript DevOps 工程师。

所以你只是在同一个句子里读了 DevOps 和 JavaScript。你是疯了还是极度好奇？无论如何，你不会经常把这两者放在一起。过去，JavaScript 被用来给网页添加一些点缀。它不可能在 DevOps 有一席之地，对吧？哦，是的，它是。

JavaScript(现在是 TypeScript)已经渗透到软件工程的每一个角落。首先，它是一个前端的东西。然后，它变成了一个后端的东西(用 Node.js)。然后是物联网。现在，我们终于带着我们的 JS 行李到达了 DevOps 火车站。从该死的火车上下来，打开行李。读完这篇文章后，你离成为 JavaScript DevOps 工程师又近了一步。

![](img/4b7027a9ae98a9ed9e82a746a70c0661.png)

*Photo by* [*Markus Winkler*](https://unsplash.com/@markuswinkler?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) *on* [*Unsplash*](https://unsplash.com/s/photos/script?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

# zx 简介

首先，我给你介绍一下 zx。这是一个让你使用 JavaScript 轻松编写脚本的库。要开始使用，您需要将它作为一个全局包安装到

```
$ npm i -g zx
```

很好，现在您已经在本地拥有了它，让我们编写第一个脚本来试用它。为了在脚本中使用 JS，我们需要放一个头，表明我们将使用 zx。因此，打开您最喜欢的编辑器，创建一个新文件`test.mjs`，并将它放在第一行:

```
#!/usr/bin/env zx
```

很好，现在让我们添加一些 JavaScript 代码:

```
#!/usr/bin/env zx

console.log("Hello from JS script")
```

让我们通过在终端中运行以下命令来使它可执行:

```
$ chmod +x test.mjs
```

然后，让我们运行脚本:

```
$ ./test.mjs
```

你的剧本问候你了吗？耶，我们成功了。如果您想将文件命名为`.js`，您需要使用不同的语法，如下所示:

```
#!/usr/bin/env zx

;(async function () {
  console.log("Hello from JS script")
})()
```

`.mjs`很方便，因为你可以使用顶级的`await`呼叫。但是使用`.js`，你需要创建一个`async`函数并使用`await there`。

您还可以使用以下命令运行脚本:

```
$ zx test.mjs
$ zx test.js
```

酷，我们复习了使用 zx 的基本知识。让我们来看看一些复杂的例子，看看 zx 真正的闪光点在哪里。我的 dotfiles 中有一个安装脚本来设置我的环境。它主要处理我每天使用的程序的安装。前阵子用 Ruby 写的，下面用 JavaScript 重写一下吧。

# zx 的真正用途

我们将创建一个脚本，为我们安装一些东西:`vim-plug ripgrep zsh`和`oh-my-zsh`一个终端主题，它还将从我的[点文件库](https://github.com/nikolalsvk/dotfiles)中复制点文件到本地磁盘上的适当位置。而且，它会给`.zshrc`增加一行。“哇，哇，哇，慢点”——你一定在想。抱歉，我有点操之过急了。我们将从安装`ripgrep`开始，学习如何从 zx 脚本运行命令。

## 运行命令

长话短说，`[ripgrep](https://github.com/BurntSushi/ripgrep)`是你的文本/正则表达式搜索伙伴。速度超快，很好用。如果你不用的话，可以去看看。在安装之前，我们先检查一下`ripgrep`是否可用。显然，如果它已经存在，我们就不想安装它。我们可以从脚本`which rg`中运行一个命令，让我们知道`ripgrep`是否存在。让我们试一试:

```
#!/usr/bin/env zx

await $`which rg`
```

将脚本保存为`install.mjs`并通过`zx install.mjs`运行。失败了吗？很好，这正是我们的目标。如果没有安装`rg`，命令`which rg`会导致脚本失败，提前退出。为什么？这就是 zx 的工作方式。你可以用`$\` some command”指定一个命令，它会返回一个承诺。基本上，它将产生一个子进程，并在那里运行指定的命令。如果命令失败，并且你没有处理失败的承诺，程序将会中断。很聪明，是吧？

好，那么我们来处理一个没有安装`rg` ( `ripgrep`)的情况。我们将`try catch`命令`which rg`并将`ripgrep`安装到`catch`模块中。我在 Mac 上，用`brew`装东西。你可以使用你使用的任何软件包管理器，我不会告诉你该怎么做，废话。让我们看看如何以编程方式安装它:

```
#!/usr/bin/env zx

console.log(chalk.blue("Checking if rg exists..."))

try {
  await $`which rg`
  console.log(chalk.green("You already have rg, awesome!"))
} catch {
  console.log(chalk.red("Nope, installing rg (rigrep)"))

  await $`brew install ripgrep`
}
```

看起来很整洁，是吧？尝试将这段代码保存到`install.mjs`文件中，并使用`zx install.mjs`运行它。您注意到的第一件事将是一个蓝色文本，上面写着“正在检查 rg 是否存在……”。哇，颜色。是的，你可以使用 zx 自带的`chalk`,在旅途中给你的输出文本上色。

如果你没有`rg`，你会在你的终端得到一个红色的文本，后面是负责安装`ripgrep`的命令输出。同样，如果你在 Linux 上，你可以用`apt`甚至`sudo apt`代替`brew`。你最了解你的系统。

如果你有 rg 可执行文件，它会打印出“你已经有 rg 了，太棒了！”绿色文本，我们可以开始下一步了。

## 不抛出异常

我们现在将从`zx`开始探索`nothrow`方法。为了展示我们如何做到这一点，让我们首先尝试实现将`.vimrc`从 [my dotfiles](https://github.com/nikolalsvk/dotfiles) 复制到主目录中的系统`.vimrc`。

想法是让`install.mjs`将`.vimrc`复制到`~/.vimrc`，但是它应该询问用户是否想要覆盖现有的`~/.vimrc`。我们可以用`cp -i`命令很容易地做到这一点，该命令将询问您是否希望覆盖您要复制到的目标。下面是对`-i`标志的解释:

```
$ man cp

...

     -i    Cause cp to write a prompt to the standard error output before copying a file that would overwrite an existing file. If the
           response from the standard input begins with the character ‘y’ or ‘Y’, the file copy is attempted. (The -i option overrides any
           previous -n option.)

...
```

让我们在`install.mjs`中这样做:

```
#!/usr/bin/env zx

console.log(chalk.blue("Copying .vimrc to ~/.vimrc"))
await $`cp -i .vimrc ~/.vimrc`
```

保存文件并运行`zx install.mjs`。如果第一次运行时没有文件，就不会得到覆盖提示。但是，如果您重新运行它，它会询问您是否要覆盖——输入`n`表示否将会停止脚本。为什么？嗯，`cp -i .vimrc ~/.vimrc`像这样返回退出代码 1:

```
$ zx test.mjs
Copying .vimrc to ~/.vimrc
$ cp -i .vimrc ~/.vimrc
overwrite ~/.vimrc? (y/n [n]) n
not overwritten
Error: overwrite ~/.vimrc? (y/n [n]) not overwritten
    at file:///Users/.../test.mjs:4:8
    exit code: 1
```

您的第一个想法一定是——让我们做一个`try catch`阻塞，阻止该命令结束我们的脚本。你是对的，这是可行的。但是，我们想在这里尝试一下`nothrow`方法。让我们像这样包装我们的命令:

```
#!/usr/bin/env zx

console.log(chalk.blue("Copying .vimrc to ~/.vimrc"))
await nothrow($`cp -i .vimrc ~/.vimrc`)
```

然后，当我们运行`zx install.mjs`时，我们得到:

```
$ zx test.mjs
Copying .vimrc to ~/.vimrc
$ cp -i .vimrc ~/.vimrc
overwrite /Users/nikolalsvk/.vimrc? (y/n [n]) n
not overwritten
```

所以`nothrow`不会让我们的脚本戛然而止，它会默默忽略“失败”的命令。多整洁啊！我们能在这做点别的吗？你打赌我们能。准备好参加有奖游戏。

## 奖励回合:获得操作系统主目录

在前面的例子中，我们大量使用了`~/`。我们怎样才能让它变得更不可知论和“正确”？幸运的是，我们可以使用`os.homedir()`来拯救我们，并确保我们的安全。对吗？没错。让我们稍微重构一下代码来使用它。

```
#!/usr/bin/env zx

const homeDir = os.homedir()
console.log(chalk.blue(`Copying .vimrc to ${homeDir}/.vimrc`))
await nothrow($`cp -i .vimrc ${homeDir}/.vimrc`)
```

哦，哇，但是它会起作用吗？你知道这个练习，保存文件，然后运行`zx install.mjs`。您应该会得到类似下面的内容:

```
$ zx test.mjs
Copying .vimrc to /Users/nikolalsvk/.vimrc
$ cp -i .vimrc /Users/nikolalsvk/.vimrc
overwrite /Users/nikolalsvk/.vimrc? (y/n [n]) n
not overwritten
```

现在每个阅读你的 JS 脚本的人都会——我很幸运认识/雇佣/工作/和这个人一起出去，因为你是如此的可爱和体贴。但是玩笑归玩笑，这里一个很好的事情是你不需要显式地导入`os`来使用它，`zx`已经为我们做了，这导致了一个干净简洁的脚本来复制文件。谢谢，`zx`，你摇滚了。

让我们试试`zx`的另一个特性——提问的能力。

## 问问题

让我们使用之前复制文件的例子，但是让我们编写我们的逻辑，询问用户是否想要覆盖文件。感谢`zx`，我们有了可以使用的`question`方法。让我们这样试一下:

```
#!/usr/bin/env zx

const homeDir = os.homedir()

console.log(chalk.blue(`Copying .vimrc to ${homeDir}/.vimrc`))

if (fs.exists(`${homeDir}/.vimrc`)) {
  const overwrite = await question(
    `Do you want to overwrite ${homeDir}/.vimrc? (y/n [n]) `
  )

  if (overwrite.toLowerCase().startsWith("y")) {
    console.log(chalk.green(`Overwriting ${homeDir}/.vimrc`))
    await $`cp .vimrc ${homeDir}/.vimrc`
  } else {
    console.log(chalk.blue(`Not overwritting ${homeDir}/.vimrc`))
  }
} else {
  await $`cp .vimrc ${homeDir}/.vimrc`
}
```

这里发生了很多事情。我们首先检查`${homeDir}/.vimrc`是否存在。如果是，我们会询问用户是否想要覆盖它。如果小写答案与“y”匹配，我们将覆盖文件。如果没有，我们打印出脚本不会覆盖文件。最后，如果没有`${homeDir}/.vimrc`，我们调用基本的`cp`命令，而没有之前的内置提示。

如果我们运行脚本并说“y”，则输出如下:

```
$ zx test.mjs
Copying .vimrc to /Users/nikolalsvk/.vimrc
Do you want to overwrite /Users/nikolalsvk/.vimrc? (y/n [n]) y
Overwriting /Users/nikolalsvk/.vimrc
$ cp .vimrc /Users/nikolalsvk/.vimrc
```

如果我们输入其他内容或按 enter 键，我们会得到以下结果:

```
$ zx test.mjs
Copying .vimrc to /Users/nikolalsvk/.vimrc
Do you want to overwrite /Users/nikolalsvk/.vimrc? (y/n [n])
Not overwritting /Users/nikolalsvk/.vimrc
```

酷，我们现在已经完成了几乎所有的`zx`的基本功能，使用起来很容易。

# 其他功能

我们在安装脚本中介绍了几个例子。让我们看看还有什么。

## 你能把那东西给我吗？

您还可以使用`fetch`来获取任何 URL。尝试使用:

```
#!/usr/bin/env zx

const response = await fetch("https://api.github.com/octocat")
console.log(await response.text())
```

运行之后，我得到了以下结果:

```
$ zx fetch.mjs
$ fetch https://api.github.com/octocat

               MMM.           .MMM
               MMMMMMMMMMMMMMMMMMM
               MMMMMMMMMMMMMMMMMMM      ____________________________
              MMMMMMMMMMMMMMMMMMMMM    |                            |
             MMMMMMMMMMMMMMMMMMMMMMM   | Keep it logically awesome. |
            MMMMMMMMMMMMMMMMMMMMMMMM   |_   ________________________|
            MMMM::- -:::::::- -::MMMM    |/
             MM~:~ 00~:::::~ 00~:~MM
        .. MMMMM::.00:::+:::.00::MMMMM ..
              .MM::::: ._. :::::MM.
                 MMMM;:::::;MMMM
          -MM        MMMMMMM
          ^  M+     MMMMMMMMM
              MMMMMMM MM MM MM
                   MM MM MM MM
                   MM MM MM MM
                .~~MM~MM~MM~MM~~.
             ~~~~MM:~MM~~~MM~:MM~~~~
            ~~~~~~==~==~~~==~==~~~~~~
             ~~~~~~==~==~==~==~~~~~~
                 :~==~==~==~==~~
```

## `cd`你回家的路

您可以使用`cd`命令轻松地在文件系统中移动。让我们打印出您(可能)不知道您的 Unix 系统上有《指环王》日历:

```
#!/usr/bin/env zx

cd("/usr/share/calendar")

await $`cat calendar.lotr`
```

你至少应该看到这一部分:

```
01/05   Fellowship enters Moria
01/09   Fellowship reaches Lorien
01/17   Passing of Gandalf
02/07   Fellowship leaves Lorien
02/17   Death of Boromir
02/20   Meriadoc & Pippin meet Treebeard
02/22   Passing of King Elessar
02/24   Ents destroy Isengard
02/26   Aragorn takes the Paths of the Dead
03/05   Frodo & Samwise encounter Shelob
03/08   Deaths of Denethor & Theoden
03/18   Destruction of the Ring
03/29   Flowering of the Mallorn
04/04   Gandalf visits Bilbo
04/17   An unexpected party
04/23   Crowning of King Elessar
05/19   Arwen leaves Lorien to wed King Elessar
06/11   Sauron attacks Osgiliath
06/13   Bilbo returns to Bag End
06/23   Wedding of Elessar & Arwen
07/04   Gandalf imprisoned by Saruman
07/24   The ring comes to Bilbo
07/26   Bilbo rescued from Wargs by Eagles
08/03   Funeral of King Theoden
08/29   Saruman enters the Shire
09/10   Gandalf escapes from Orthanc
09/14   Frodo & Bilbo's birthday
09/15   Black riders enter the Shire
09/18   Frodo and company rescued by Bombadil
09/28   Frodo wounded at Weathertop
10/05   Frodo crosses bridge of Mitheithel
10/16   Boromir reaches Rivendell
10/17   Council of Elrond
10/25   End of War of the Ring
11/16   Bilbo reaches the Lonely Mountain
12/05   Death of Smaug
12/16   Fellowship begins Quest
```

还有几个`zx`的特性，你可以在 GitHub 的[官方回购上查看。自述文件非常详细，无论您想要构建什么，它都能为您提供广泛的帮助。](https://github.com/google/zx)

# 总结

感谢你读到这里，这对我意义重大。今天我们学到了很多关于`zx`的知识。你现在离成为一名 JavaScript DevOps 工程师更近了一步，恭喜你🎉。你已经感到自豪和富有成效了吗？很好，很高兴我帮了忙。

我们看了一下`zx`的几个特点:

*   用`$\`命令调用命令的能力` --它将产生一个你需要等待的进程。它还会抛出一个您需要捕捉的异常，所以要小心。
*   有`nothrow`可以确保命令不会破坏你的脚本。
*   我们学习了`questions`以及如何让你的脚本具有交互性。
*   有`fetch`从网上获取网址(也许是本地的？)
*   可以用`cd`导航。

这就是这篇博文的全部内容。加入[时事通讯](https://pragmaticpineapple.com/newsletter)，因为我计划以打字稿的形式完成所有这些工作。是的，每个人都在重写他们的代码库。另外，如果你喜欢 DevOps JS 的想法，请告诉我，我会写更多关于它的内容。

你可以在 GitHub 上的[我的点文件](https://github.com/nikolalsvk/dotfiles)中找到我从 Ruby 转换成 JavaScript 的脚本。下面是[完整的](https://github.com/nikolalsvk/dotfiles/blob/master/install.mjs) `[install.mjs](https://github.com/nikolalsvk/dotfiles/blob/master/install.mjs)` [文件](https://github.com/nikolalsvk/dotfiles/blob/master/install.mjs)。如果你喜欢，留下一颗星星。如果没有，请迅速关闭浏览器选项卡。

考虑与你的朋友和同事分享这篇博文。也许有人只是在等待这种类型的内容。在 Twitter 上有一个快速的方法:

这就是我今天给你的全部。下次再见。

干杯。

*原载于 2022 年 3 月 15 日 https://pragmaticpineapple.com**的* [*。*](https://pragmaticpineapple.com/devops-javascript-intro-to-writing-scripts-with-zx/)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*