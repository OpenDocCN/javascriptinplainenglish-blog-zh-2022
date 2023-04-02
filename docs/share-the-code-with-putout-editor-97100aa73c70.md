# 与共享代码🐊输出编辑器

> 原文：<https://javascript.plainenglish.io/share-the-code-with-putout-editor-97100aa73c70?source=collection_archive---------12----------------------->

## 了解输出编辑器的这一新功能。

![](img/606d981e35ba9de0f534c035db4207bf.png)

*The whip and rope are necessary,
Else he might stray off down
some dusty road.
Being well-trained, he becomes
naturally gentle.
Then, unfettered, he obeys his master.
© Zen Ten Bulls*

嗨伙计们！当你写插件的时候🐊有很多事情需要考虑:

*   🤷‍♂️如何在`[AST](https://github.com/estree/estree)`中调用 JavaScript 的一部分？
*   🤷‍♂️用什么[类型的插件](https://github.com/coderaiser/putout/tree/v24.5.0/packages/engine-runner#supported-plugin-types)呢？
*   🤷‍♂️如何快速检查所有边缘案例的转换？

所有这些问题都有一个答案，🥁:

> **☝️🐊**T2**！**

它已经存在了很长一段时间，但现在有能力共享代码☘️！

例如，您可以[编辑](https://putout.cloudcmd.io/#/gist/1218cbc539f3a9c0d238c7793d0ee156/73ef140be579f6faf520f76dc052d21396092ea7)一个全新的规则`[package-json/add-type](https://github.com/coderaiser/putout/tree/v24.5.0/packages/plugin-package-json#add-type)`。

# 用`package-json/add-type`添加模块类型

再谈一谈新的转变。它的作用是:

```
{
    "name": "hello",
    "version": "1.0.0",
+   "type": "commonjs"
}
```

将已使用模块的`[type](https://nodejs.org/dist/latest-v17.x/docs/api/packages.html#type)`添加到`package.json`。

他们有两个人:

*   ✅ [CommonJS](https://nodejs.org/dist/latest-v17.x/docs/api/modules.html#modules-commonjs-modules)
*   ✅ [EcmaScript 模块](https://nodejs.org/dist/latest-v17.x/docs/api/esm.html#modules-ecmascript-modules)

你是怎么问的？接下来阅读！

# 使用`operator.getProperties`获取属性

当你需要从你的`package.json`或任何`[ObjectExpression](https://babeljs.io/docs/en/babel-types#objectexpression)`或`[ObjectPattern](https://babeljs.io/docs/en/babel-types#objectpattern)`中获取属性时，你可以使用`[getProperties](https://github.com/coderaiser/putout/tree/v24.5.0/packages/operate#getpropertiespath-path-names-string)`:

```
const {homepagePath} = getProperties(__aPath, ['homepage']);
```

它需要一个`path`和一个需要遍历的`top-level`元素数组，当找到它们时，它们以`Path`前缀返回，所以你可以用任何你喜欢的方式操纵它们😏！

今天就到这里吧！玩得开心愉快[变身](https://github.com/jamiebuilds/babel-handbook/blob/master/translations/en/plugin-handbook.md#manipulation)🦉！

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***