# Vue-i18n 键回退——用函数装饰器处理丢失的键并保留选项

> 原文：<https://javascript.plainenglish.io/vue-i18n-key-fallback-handle-missing-keys-and-keep-options-with-a-function-decorator-2a67970248ee?source=collection_archive---------5----------------------->

## 使用 function decorator 模式添加一些额外的回退、错误处理程序或其他辅助操作。

![](img/4016068051b58bd5c1a1a36ff697b181.png)

Photo by [Arpit Rastogi](https://unsplash.com/@arptrastogi?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 中广泛使用的国际化库— `vue-i18n`有一些局限性。在[evonica](https://evionica.com/)中，我们遇到了对未识别的翻译键进行回退的需求。

# 平移插值

该库需要一个包含关键字和翻译字符串的本地化文件。

Example of localization file structure

基本用法非常简单——您必须传递翻译键，然后在结果中获得翻译文本。

Basic `vue-i18n` translation example

您可以插入翻译，在翻译文本中添加`{variable}`,并传递选项对象，将`{variable: 'someValue'}`作为翻译调用的第二个参数。

# 缺少翻译

当`vue-i18n`翻译功能无法识别翻译密钥时，则返回密钥本身。这个库提供了一个地方来声明在初始化器中的`missing`方法，这个方法在这种情况下被触发。`missing`方法有一个类型`MissingHandler`。

Vue-i18n missing handler type declaration

## 基本回退

您可以创建一些后备翻译。您可以在初始化器中访问`i18n`实例。在下面的情况中，当缺少翻译密钥时，返回回退密钥的翻译。

Missing handler with fallback for missing translations

## 缺少选项

不幸的是，`missing`函数不包含传递参数的信息。如果您想访问它们，您必须后退一步，在函数调用之前收集它们。

为此，您可以创建一个自定义函数装饰器。函数装饰器获取原始函数，执行一些辅助操作，然后执行原始函数。

Examples of basic function decorators with or without arguments

正如你在第二个例子中看到的，有对参数的访问。翻译键总是所有`i18n.global.t`重载中的第一个参数。

你可以析构参数，得到你想要保留的`key`和`rest`。当转换函数返回键时，让我们调用回退键的转换，传递所有其他原始参数。

Missing translation decorator

如果要添加类型脚本类型:

Typed missing translation decorator

# 摘要

使用 function decorator 模式，您可以对函数结果进行预处理或后处理，添加一些额外的回退、错误处理程序或其他辅助操作。我们使用它们来允许在配置文件中声明未知的键。我们不必担心丢失翻译输出，因为有一个后备方案。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*