# Git 中的 Rebases 以及为什么不应该害怕它们

> 原文：<https://javascript.plainenglish.io/rebases-in-git-and-why-you-shouldnt-be-afraid-of-them-b36a1bdccadf?source=collection_archive---------7----------------------->

![](img/992a7b2f486d0d928577bdf0250eadb0.png)

Illustration by the author

初学者在使用 Git 时经常会对 rebases 有几点困惑:

在本文中，我将提供这些问题的答案。其间，TL；DR:rebase 是一种将你的原始提交历史变成你想与你的团队其他成员分享的东西的方法。

# 如何做一个 rebase

要执行重定基础，您可以运行`git rebase <commit-reference>`。提交引用可以是任何内容，例如:

*   分行名称，
*   标签，或者
*   提交 id。

重定基础是一个相当复杂的操作，所以让我们来看一下它的各个方面。

# 简单重置基础

在其最简单的形式中，重定基础从一个地方(一个基础)取得变化，并将它们移动到另一个地方。它改变了历史分叉的地方。因此，对于我之前[所写的树别名](https://how-to.dev/how-to-display-git-branches-as-a-tree-in-cli)，我们从这样的分支图开始:

```
$ git tree
* 293b722 (HEAD -> test) add test.txt file
| * abc01e7 (origin/main, origin/HEAD, main) Add lorem ipsum to readme
|/
* edd3504 Add readme
```

我们移动我们的分支从不同的地方开始——主分支的顶部:

```
$ git rebase main
Successfully rebased and updated refs/heads/test.
```

结果，我们得到了这样一棵树:

```
$ git tree
* fe4254e (HEAD -> test) add test.txt file
* abc01e7 (origin/main, origin/HEAD, main) Add lorem ipsum to readme
* edd3504 Add readme
```

我们的`test`分公司以前是从`edd3504 Add readme`开始，现在是从`abc01e7 Add lorem ipsum to readme`开始。

# 重定基础正在进行中

即使是简单的重定基数也可能需要你方的额外投入。例如，您可能需要解决一些冲突:

```
$ git rebase main
Auto-merging test.txt
CONFLICT (add/add): Merge conflict in test.txt
error: could not apply 293b722... add test.txt file
hint: Resolve all conflicts manually, mark them as resolved with
hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
hint: You can instead skip this commit: run "git rebase --skip".
hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
Could not apply 293b722... add test.txt file
```

在这种情况下检查状态时，您将从 Git 获得如何继续的指示:

```
$ git status
interactive rebase in progress; onto a03989b
Last command done (1 command done):
   pick 293b722 add test.txt file
No commands remaining.
You are currently rebasing branch 'test' on 'a03989b'.
  (fix conflicts and then run "git rebase --continue")
  (use "git rebase --skip" to skip this patch)
  (use "git rebase --abort" to check out the original branch)

Unmerged paths:
  (use "git restore --staged <file>..." to unstage)
  (use "git add <file>..." to mark resolution)
        both added:      test.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

您需要编辑该文件来解决冲突。完成后，将更改添加到暂存中:

```
$ git add test.txt
(no output)
```

你继续重定基数:

```
$ git rebase --continue
[detached HEAD b81cad4] add test.txt file
 1 file changed, 1 insertion(+)
Successfully rebased and updated refs/heads/test.
```

随后，Git 将继续 rebase:它可以顺利完成，就像我的情况一样，或者您可能会遇到更多需要手动解决的冲突。

# Rebase 交互式

rebase 的一个更高级的选项是 rebase interactive。它允许你在树枝上做非常精确的改变——不仅仅是把它从一个地方移到另一个地方。下面我们来看几个例子。

## 改写提交

您可以做的最简单的事情就是更改提交消息。好的一面是没有冲突的机会，因为文件保持不变。

## 挤压提交

你可以选择几个提交，把它们变成一个。它保留了文件的更改——它只是将一连串的更改合并到一次提交中。它需要为新的提交写一个新的提交消息，但是它本身不会引起冲突。

## 编辑提交

您也可以在提交中编辑文件更改。这允许您确保提交包含所有相关的更改。如果稍后在分支中对相同的位置进行了更改，那么您将需要手动解决冲突。

## 删除提交

另一个操作是从分支中删除提交——提交及其更改。如果稍后在分支中对相同的代码进行了额外的修改，删除提交将导致一些冲突。最基本的用例是当你意识到一些改变是不需要的，你想从历史中删除它们。除此之外，当我意识到我的分支变得太大时，我经常使用它，我打算让它更集中，并尽快合并它。

## 重新排序提交

您也可以对提交进行重新排序。在某些情况下，这可能是有意义的，但是如果您试图重新排序一个更改了相同代码区域的提交，它会很快变得复杂。

# 文件接口

正如你所看到的，交互式重定基础需要很多微妙的输入。Git 以文本文件的形式获取这个输入。当我运行`git rebase main -i`时，我得到了包含以下内容的编辑器:

```
pick a03989b add test.txt

# Rebase abc01e7..a03989b onto abc01e7 (1 command)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
# .       specified); use -c <commit> to reword the commit message
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
```

当您保存文件并退出编辑器时，Git 将遵循您在那里提供的说明。这是一个界面，一开始可能会觉得很笨拙，但你可以很快习惯它。唯一的“问题”是您需要知道您的默认编辑器，并知道如何使用它。我已经在[的另一篇文章](https://how-to.dev/how-to-keep-your-sanity-while-working-with-git#heading-check-what-your-default-editor-is)中写了更多。

# 实用技巧

在做交互重基础的时候，尽量一次做一件事。Git 可以在一个 rebase 中完成以下工作:
更改分支起点

*   重新排序一些提交
*   压扁别人
*   等等。

然而，你可能会迷失在所有同时发生的冲突中。一次只做一件事，保持以下顺序更容易:

*   首先删除多余的提交，
*   挤压相关的提交，然后
*   把树枝移到另一个基地。

通过这种方式，您减少了必须来回移动的提交数量——从而减少了必须解决的冲突数量。

# 历史在改变

重置基础会改变存储库的历史。这意味着相同的更改将作为不同分支上的不同提交出现。这不是一个错误，但当您第一次看到以下日志时，可能会感到困惑:

```
$ git push origin test
To github.com:how-to-js/git.md.git
 ! [rejected]        test -> test (non-fast-forward)
error: failed to push some refs to 'github.com:how-to-js/git.md.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details
```

`non-fast-forward`表示从存储库历史中的一点到另一点没有直接的路径。在这种情况下，您需要自己集成远程和本地更改。同步分支有一些微妙之处，这是另一篇文章的主题。

根据项目中的工作流，可以禁止或要求覆盖某些分支的历史记录。我使用的工作流禁止对 master/main 分支进行历史更改，并且它需要所有其他分支的 rebases。重定基础的方法没有对错之分:每种策略都有其利弊，但很可能您的团队会坚持您与所选方法保持一致。

# 可能的副作用

除了 rebases 固有的复杂性之外，它们还在团队环境中引入了一些挑战:

# 仅限本地的分支机构

当你的工作只在你的电脑上时，以任何其他方式改变历史总是安全的。这是一个很好的做法，因为它总是能帮助你在别人看到你的工作之前清理干净。如果您在一个月前开始了一些工作，并且从那时起，您已经定期地对 main 进行了更改——不值得用像`Merge remote-tracking branch 'origin/main' into test`这样的提交来保存信息。相反，你可以定期调整基数，将历史记录保持为一条直线。

# 上传到远程的分支

一旦你分享了你的分支，对它的历史的任何改变都可能破坏东西。例如，您的持续集成(CI)将记住提交的测试运行的结果，但是提交将会消失。我遇到过一些人，他们对改变已经共享的历史非常谨慎，所以我想有些团队可能不鼓励这样做。

# 其他人工作的远程分支

最复杂的情况是改变其他人正在处理的分支的历史。为此，我建议:

*   当变更发生时，确保每个人都是最新的——没有两个人同时向分支引入变更；
*   在开始新的工作之前，让每个人都更新到新的、重新确定基础的分支。

这是一个微妙的情况，因为它破坏了 Git 使用的许多自动化冲突解决方案。在这种情况下，最好小心谨慎，确保每个人都知道发生了什么。

# 坚持学习

如果你有兴趣学习更多关于 Git 分支的知识，可以在 [Learn Git Branching](https://learngitbranching.js.org/) 找到一个很棒(也很漂亮)的资源。如果你有兴趣了解更多关于 Git 的知识，在这里注册[来获取我的 Git 相关内容的更新。](https://how-to-dev.ck.page/e92d2eb5d7)

*原发布于*[*https://how-to . dev*](https://how-to.dev/rebases-in-git-and-why-you-shouldnt-be-afraid-of-them)*。*

*更多内容请看* [***说白了。***](https://plainenglish.io/)

*报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) ***。***

***有兴趣缩放你的软件启动*** *？检查* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。*