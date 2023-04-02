# npm 安装—如何在特定条件下最大限度地减少其使用

> 原文：<https://javascript.plainenglish.io/npm-install-how-to-minimize-its-use-under-specific-conditions-1e6dada6fa61?source=collection_archive---------13----------------------->

## 从长远来看可以节省时间。

![](img/9acf349ad7f435108a0c754e619a5394.png)

Photo by [Natali_Mis](https://www.istockphoto.com/portfolio/Natali_Mis)

## 要求:

1.  你在做一个项目吗？
2.  每次创建新的分支都必须运行`npm install`吗？
3.  是否需要看似短暂的永恒才能完成？
4.  你是否受够了，想要节省时间？

如果你对这些问题的回答是肯定的，那么这是给你的！

# **救援的象征性链接**

我们可以将依赖项保存在一个单独的中心文件夹中，而不是每次创建新的分支时都安装依赖项。然后，我们可以在中心文件夹中创建指向`node_modules`的符号链接:

1.  运行`npm install`生成`node_modules`。
2.  在不同的位置创建一个文件夹，比如说 Windows 的`C:\project-deps`**或者 Linux 的`/home/project-deps`。**
3.  **剪切粘贴`node_modules`到那个文件夹。**
4.  **在分支的文件夹位置打开 PowerShell 或命令提示符(或 Linux 的终端)。**
5.  **创建符号链接。
    **对于 Windows(PowerShell):**`cmd /c mklink /J node_modules C:\project-deps\node_modules` **对于 Windows(命令提示符):** `mklink /J node_modules C:\project-deps\node_modules` **对于 Linux:** `ln -s /home/project-deps/node_modules node_modules`**

**就是这样！NodeJS 会将`node_modules`视为位于您的分支文件夹中。从现在开始，您只需要检查一个分支，运行命令来创建符号链接，就可以开始了！**

# **维护依赖关系**

**在某些时候，您或团队的其他成员可能会添加新的依赖项。不幸的是，通过符号链接从我们分支的文件夹中安装新的依赖项并不像我们希望的那样工作。**

**虽然`node_modules`被 NodeJS 识别为执行，但不被识别为安装。它将安装所有东西，就像`node_modules`不存在一样。**

**如果您需要安装新的依赖项:**

1.  **将新的`package.json`文件复制粘贴到中心文件夹中。**
2.  **如果存在旧版本，选择覆盖。**
3.  **运行`npm install`。**

**对于一个相对较小的项目，第一次运行生成`node_modules`花费了 250.145 秒。后续运行花费的时间要少得多(大约 25 秒)，但是这完全取决于所安装的依赖项的大小。**

**最后，在删除合并的分支时，我们也节省了时间——要删除的文件越少，意味着删除速度越快。**

# **结论**

**在本文中，我们看到了如何通过使用符号链接来跳过运行`npm install`并节省时间。我希望这有助于加快你的进度。**

**编码快乐！**

***更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。***