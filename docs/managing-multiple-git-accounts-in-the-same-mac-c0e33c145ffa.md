# 在同一台 Mac 上管理多个 Git 帐户

> 原文：<https://javascript.plainenglish.io/managing-multiple-git-accounts-in-the-same-mac-c0e33c145ffa?source=collection_archive---------2----------------------->

![](img/1402b485de26f2963f05901c45a14977.png)

Photo by RealToughCandy.com: [https://www.pexels.com/photo/man-love-people-woman-11035539/](https://www.pexels.com/photo/man-love-people-woman-11035539/)

把你的专业工作和个人工作分开是个好主意。最好的方法是使用工作笔记本电脑和个人笔记本电脑。

但是你可能经常想在你的工作笔记本上快速尝试一些私人的事情，比如查阅你的学习项目或者尝试一个新的图书馆。

您可能面临的主要问题是管理您的 git 档案，并确保您不会意外地将您的工作设置推送到您的个人帐户，反之亦然。

在每个 git 命令中使用 git 帐户是令人生畏的。

我想把我所有的个人项目放在一个`~/personal-directory`里，这样就有了明确的界限。我希望当我在我的`~/personal-directory`中时，我的系统自动识别我的个人 git 配置文件，并在系统的其他地方识别我的工作 git 配置文件

您可以通过以下配置轻松实现这一点

使用命令创建[不同的密钥](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

```
ssh-keygen -t ed25519 -C “your_personal_email@example.com”ssh-keygen -t ed25519 -C “your_work_email@example.com”
```

用不同的名字保存每把钥匙，比如工作用的`id_ed25519`，私人用的`id_ed25519_personal`。这将为~/中的两个帐户创建您的私钥和公钥。ssh 目录

现在将您的[公钥添加到您的账户档案](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)中。

打开~/。gitconfig

替换~/中的[用户]设置。gitconfig 包含以下内容

```
[include]
     path = ~/git_work.conf
[includeif "gitdir:~/personal-directory/"]
     path = ~/git_personal.conf
```

Create ~/git_work.conf

```
[user]
  name = Work Name
  email = work@email.com

[core]
  sshCommand = "ssh -i  ~/.ssh/id_ed25519"
```

Create ~/git_personal.conf

```
[user]
  name =Personal Name
  email = personal@email.com

[core]
  sshCommand = "ssh -i  ~/.ssh/id_ed25519_personal"
```

现在在你的`~/personal-directory`里做一个`git init`

此后，你在 personal-directory 中的所有 git 活动都将使用你的个人配置文件和密钥。在系统中的其他地方，它将使用您的工作配置文件和密钥。

要进行验证，请在您的`personal-directory`中运行以下命令

```
git config --show-origin user.email
```

这应该显示您的个人电子邮件

如果您在个人目录之外的任何 repo 中运行相同的命令，它应该会给您的工作电子邮件

参考

[在 MacOs 上处理多个 Github 账户](https://gist.github.com/Jonalogy/54091c98946cfe4f8cdab2bea79430f9)

[core.sshCommand](https://git-scm.com/docs/git-config#Documentation/git-config.txt-coresshCommand)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***