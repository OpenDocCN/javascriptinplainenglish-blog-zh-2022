# 如何使用 Git 穿越时间

> 原文：<https://javascript.plainenglish.io/how-to-use-git-to-travel-through-time-a9981582b31c?source=collection_archive---------11----------------------->

![](img/1402b485de26f2963f05901c45a14977.png)

Photo by RealToughCandy.com: [https://www.pexels.com/photo/man-love-people-woman-11035539/](https://www.pexels.com/photo/man-love-people-woman-11035539/)

这篇文章将教你如何获得食物…看到我做了什么吗？不过说真的，Git 对于软件开发人员来说是一个非常有价值的工具，可以跟踪他们的代码和状态。Git 有很多不同的命令，其中很多，我们大多数人可能因为很多不同的原因而不使用，比如我们不知道它们是做什么的，我们从来没有听说过它们，或者它们只是很可怕。

我在这里向您展示几个 git 命令，当有人不可避免地在主分支上搞砸了 git 历史、删除了 commit 以及您可能想到的任何其他灾难性情况时，这些命令可以帮助您挽救您的工程团队。所以系好安全带，我们出发吧。

**** * *注:*** *我将向您展示一些命令的基本用法，让您了解它们在日常工作中的实际应用。但是，我将链接每个命令的官方文档，以便您可以看到调用命令的所有不同方式！*

## git 日志

[](https://git-scm.com/docs/git-log) [## Git - git-log 文档

### p -u - patch 生成修补程序(请参见生成修补程序一节)。-s -无补丁…

git-scm.com](https://git-scm.com/docs/git-log) 

使用 **git log** 最简单的方法就是在 repo 中的任何分支上键入 **git log** 。它将按照从最近到最早提交的顺序，向您显示已经被推送到该分支的提交的历史。

该命令的输出如下所示:

```
$ git log
commit ca82a6dff817ec66f44342007202690a93763949
Author: John Doe <jdoe-mail.com>
Date:   Mon Mar 17 21:52:11 2008 -0700

    Change version number

commit 085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7
Author: John Doe <jdoe-mail.com>
Date:   Sat Mar 15 16:40:33 2008 -0700

    Remove unnecessary test

commit a11bef06a3f659402fe7563abf99ad00de2209e6
Author: John Doe <jdoe-mail.com>
Date:   Sat Mar 15 10:31:28 2008 -0700

    Initial commit
```

这里需要注意的重要事项是，您可以看到每次提交的提交消息和提交 SHA，我们稍后将把它们与 **git checkout** 结合起来，以实现时间旅行🕒。

## git 检验

[](https://git-scm.com/docs/git-checkout) [## git-git-签出文档

### 安静安静，抑制反馈信息。- progress - no-progress 在标准错误上报告进度状态…

git-scm.com](https://git-scm.com/docs/git-checkout) 

因此， **git checkout** 最常用于创建新分支或切换到现有分支。但是 git checkout 还有一个较少使用的选项，那就是…

```
git checkout <commit-sha>
```

此命令允许您签出分支历史中的任何提交。为什么这很酷？以下面的例子为例。

```
Branch Aabc1 -- abc2 -- abc3git checkout abc2
```

所以，你有一个分支 A，你意识到可能有一个更有效的方法在代码中写一个昂贵的函数，但是你还不想提交它。所以你决定要回到分支的旧状态，你做了一个 **git checkout abc2** 来返回提交 **abc2。**此时，git 会告诉你，你处于一个分离的 head 状态，这只是一种奇特的说法，说明你已经在你签出的提交中创建了你的分支的沙盒环境。现在，您可以尝试重写这个昂贵的函数，而不用担心弄乱分支的实际历史，除非您认为这样做是值得的。

如果您不确定如何找到能够使用该命令的提交 sha，请参考我的 **git 日志**部分。使用 log 命令时会打印提交 sha！

## git 参考日志

[](https://git-scm.com/docs/git-reflog) [## Git - git-reflog 文档

### 该命令采用各种子命令，以及取决于子命令的不同选项:git reflog [show] [ ] [ ]git…

git-scm.com](https://git-scm.com/docs/git-reflog) 

在我看来， **reflog** 是 **git log** 更强大的版本。 **reflog** 是 **HEAD** 指向的提交列表。在 Git 世界中，这是你能找到的最接近摆脱困境的方法。命令输出如下所示…

```
git reflog
e1bec01 HEAD@{1}: commit: Set up ui for progress bar
f390e95 HEAD@{2}: commit: Updated README 
7a8682a HEAD@{3}: commit: Hooked up Express Server
```

数字串再次成为我们已经学过的提交 SHA，它对于用其他命令遍历 git 历史是至关重要的。Reflog 会告诉你何时切换到其他分支，何时开始和完成 rebases，以及许多其他事情。比方说，你弄乱了一个 rebase，因为有大量的代码冲突。你可以使用一个 reflog 来重置你的头回到提交权之前，你开始你的 rebase，并再次尝试！

## git 重置

[](https://git-scm.com/docs/git-reset) [## Git - git 重置文档

### 在前三种形式中，将条目从复制到索引。在最后一个表单中，将当前分支头(head)设置为…

git-scm.com](https://git-scm.com/docs/git-reset) 

许多开发人员害怕 reset 命令，因为在它的一些变体中，它确实会删除工作分支中的更改，而删除代码会让一些人害怕。我在这里说，git reset 是你的朋友而不是你的敌人。有大量的选项可以使用它，但对于如何使用的一些基本示例，请考虑以下内容。

```
1\. git reset --HARD
2\. git reset --soft ^HEAD
```

1.  假设您尝试从远程获取分支上的最新更改，这会导致大量冲突，您只想清理本地分支并将其恢复到运行 git pull 之前的状态。git reset——hard 将重置您的本地工作更改，并将您的分支尖端指向头部。
2.  当您想要撤销或修复刚刚在分支上进行的提交时，第二个命令非常有用。它将撤销之前在分支上所做的提交，但是将更改保留为本地工作更改，以便您可以重做提交消息，对代码进行更多的更改，等等。

## git 还原

[](https://git-scm.com/docs/git-revert) [## Git - git-revert 文档

### git-revert 上次更新于 2.37.1 git-revert - Revert 一些现有的提交 git revert [ - [no-]edit] [-n] [-m…

git-scm.com](https://git-scm.com/docs/git-revert) 

这个命令非常简单，对于撤销错误的提交非常有用。

```
git revert <commit-sha>
```

假设 commit-123 引入了一个 bug，它完全破坏了生产应用程序中的一整页。

`git revert commit-123`将撤销该提交中所做的所有更改，并允许您提交回复到分支中，以完成“撤销”。许多公司都将 revert 命令作为“修复生产工作流程”的一部分。

## 结论

当然，还有更多的 git 命令可以用来浏览您的 git 历史时间线，但这是我最常用的几个命令，而且很容易学会。希望这能帮助你成为你的团队需要的英雄，下次有人搞乱项目的 git 历史，需要 Git 专家的时候。或者至少，它将帮助您撤销难看的提交并重写它们的消息😜。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*