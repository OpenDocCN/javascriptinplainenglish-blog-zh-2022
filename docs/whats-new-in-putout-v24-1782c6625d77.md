# 输出 v24 有什么新功能？

> 原文：<https://javascript.plainenglish.io/whats-new-in-putout-v24-1782c6625d77?source=collection_archive---------16----------------------->

## 查看输出 v24 的新特性。

![](img/0be6a3efbbcc7963cd87ac75ccd9a566.png)

Barefooted and naked of breast,
I mingle with the people of the world.
My clothes are ragged and dust-laden,
and I am ever blissful.
I use no magic to extend my life;
Now, before me, the dead trees
become alive.
© Zen Ten Bulls

嗨伙计们！是时候发布一个重要的🐊[产出](https://github.com/coderaiser/putout)超级短绒🎉！

发布仅包含重大变更。多与规则和插件有关。而且还包含了使插件代码更不容易出错的更改。

所以让派对开始吧！

# **🤷‍♂** ️ **对使用有疑问🐊熄灭？**

看看几个做同样事情的插件变体: [**林挺调试器语句**](https://putout.cloudcmd.io/#/gist/f61ba31fe534868d49eba9b946f3ed4b/5ef6863d9cf4826666782ae0eea5cb5def266bbd) **。**

❌ ESLint [无调试器](https://github.com/eslint/eslint/blob/2dc38aa653f1d5137a9abf82024c67a11620bb7c/lib/rules/no-debugger.js) : **43** 行；

❌ SWCLint [无调试器](https://github.com/swc-project/swc/blob/v1.2.138/crates/swc_ecma_lints/src/rules/no_debugger.rs) : **49** 行；

❌罗马[无调试器](https://github.com/rome/tools/blob/4d5a99ce98e987cbd03f3ab6b38fa22d00bbfe27/packages/%40romejs/js-compiler/transforms/lint/noDebugger.ts) : **28** 行；

❌ RSLint [无调试器](https://github.com/rslint/rslint/blob/v0.3.0/crates/rslint_core/src/groups/errors/no_debugger.rs) : **48** 行

✅ 🐊输出[移除调试器](https://github.com/coderaiser/putout/blob/v24.6.0/packages/plugin-remove-debugger/lib/remove-debugger.js) : **7** 行:

*明智地选择，竞争对手甚至不能解决……*🤫

# 🧨改名为`[@putout/operate](https://github.com/coderaiser/putout/tree/v24.0.0/packages/operate#readme)`的方法

这很简单。为了 API 的一致性，重命名了两个方法:

当然，当你使用它的时候，规则会为你声明。

# 🧨 `remove-process-exit`被合并为`[@putout/plugin-nodejs](https://github.com/coderaiser/putout/tree/v24.0.0/packages/plugin-nodejs#remove-process-exit)`

由于此规则与`nodejs`相关，因此被移动。因此，如果您禁用了此规则，您应该在`.putout.json`中进行以下更改:

# 🧨 `convert-top-level-return`被合并为`[@putout/plugin-nodejs](https://github.com/coderaiser/putout/tree/v24.0.1/packages/plugin-nodejs#convert-top-level-return)`

因为这条规则与`nodejs`有关，所以被移动了。如果您禁用了此规则，下面是您应该对`.putout.json`进行的更改:

# 🧨将所有`TypeScript`相关插件捆绑到`[@putout/plugin-typescript](https://github.com/coderaiser/putout/tree/v24.0.2/packages/plugin-typescript#readme)`

所有与`TypeScript`相关的规则被移到一个单独的包中。所以如果你禁用了其中一个，添加一个前缀`typescript`:

是的，里面有很多`TS`规则🐊`Putout`为了这一刻！

# 🧨禁用`[apply-array-at](https://github.com/coderaiser/putout/tree/v24.0.0/packages/plugin-apply-array-at#readme)`已从默认安装中移除

因为`array.at`支持节点`v16`和更高节点🐊`Putout`(静止)支撑`node v14`。该规则受支持，可以与以下产品一起单独安装:

```
npm i @putout/plugin-apply-array-at
```

如果您正在使用它，用以下内容更新`.putout.json`:

在这个版本中，我们的依赖项更少了！这使得安装速度有点快。

这就是所有的突破性变化！再来说说新功能。

# 关于爬行的几句话

![](img/78589e3addd7f7fcd4dd7ea5d655f846.png)

我在哪里可以找到一个忘记单词的人，这样我就可以和他说话了？
庄子

例如，当您删除变量或以任何方式操作它时，

它将通过`[merge-duplicate-imports](https://github.com/coderaiser/putout/tree/master/packages/plugin-merge-duplicate-imports#readme)`转换为:

但是当你启用了[声明未定义变量](https://github.com/coderaiser/putout/tree/master/packages/plugin-declare-undefined-variables#readme)时:你就有麻烦了！很可能会看到这样的错误消息:

```
TypeError: Cannot read properties of undefined (reading 'buildError')
```

这是`Babel`试图告诉你存在名称冲突的方式，代码包含了两个同名的变量。

事情是这样的`merge-duplicate-imports`没有借助:

它只删除旧节点并添加一个新节点。

这是一个给`[bindings](https://github.com/jamiebuilds/babel-handbook/blob/master/translations/en/plugin-handbook.md#toc-bindings)`对象添加变量的东西，所以其他插件可以确定是否声明。

但是不要担心！这种行为是固定的，甚至更多！你永远不需要考虑`AST`是否在你的插件修复后爬行。从现在开始它会爬上每一个固定点！

今天就到这里，这是[十牛](https://en.wikipedia.org/wiki/Ten_Bulls)禅马拉松的最后一天！那是疯狂的几周:)我玩得很开心。

最后还有几件事:

在 Medium/@ [coderaiser](https://medium.com/u/47c05fa2893e?source=post_page-----1782c6625d77--------------------------------) 上☝️Follow 我，并找出其他 9 头公牛是关于什么的😏。

☝️在 GitHub 上增加了明星⭐️，这很激励人！

如果你喜欢我正在做的事情，☝️会支持我。

☝️And 请记住，我总是在这里解决任何问题，你有我提出的代码😋。

干杯🥤！

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***