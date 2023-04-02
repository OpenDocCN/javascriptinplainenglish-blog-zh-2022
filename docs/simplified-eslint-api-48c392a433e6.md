# 简化的 ESLint API

> 原文：<https://javascript.plainenglish.io/simplified-eslint-api-48c392a433e6?source=collection_archive---------19----------------------->

## 使用和测试 ESLint 插件最简单的方法。

![](img/abc7582fafc17b51b5b9dd8768883ac6.png)

Whip, rope, person, and Ox -
all merge in No Thing.
This heaven is so vast,
no message can stain it.
How may a snowflake exist
in a raging fire.
Here are the footprints of
the Ancestors.
© Zen Ten Bulls

大家好:)！

`[ESLint](https://eslint.org/)`在以下情况下开始作为格式化程序工作🐊完成了他的转变。这就是为什么它在应用程序的不同部分被大量使用的原因，用于测试目的和以最简单的方式使用`API`。

# 为什么要简化？

“为什么要简化？”——你可以问—“这已经够简单了！”。没有你一开始想的那么简单。[这里是](https://eslint.org/docs/developer-guide/nodejs-api#-eslintlinttextcode-options)你可以使用`ESLint`的所有方式，可能的特性列表非常大。首先你需要创建`ESLint`的实例，然后计算选项，最后是 lint。[需要记忆和处理的事情](https://github.com/coderaiser/putout/blob/v24.6.0/packages/putout/lib/cli/eslint/index.js)太多，所以`API`被简化了。

# 我们开始吧

您可以通过以下方式访问它:

用法很简单:

难道它看起来不像🐊`Putout`方式？绝对是！但是...你应该记住它有几个不同之处:

*   ☝️ [*🐊*](https://github.com/coderaiser/putout#plugins) `[*Putout*](https://github.com/coderaiser/putout#plugins)` [*用*](https://github.com/coderaiser/putout#plugins) `[*code*](https://github.com/coderaiser/putout#plugins)` [*和*](https://github.com/coderaiser/putout#plugins) `[*places*](https://github.com/coderaiser/putout#plugins)` [*属性*](https://github.com/coderaiser/putout#plugins) *返回对象。*
*   ☝️ `*ESLint*` *有一个* `*name*` *属性，用于计算配置文件。*

在`config`属性的帮助下，您甚至可以覆盖任何`ESLint`选项⚙️:

如果你想申请🐊`Putout`转换使用`putout/putout` `ESLint`规则，启用`putout`与被调用标志相同:

默认情况下禁用，因为`ESLint`总是在🐊`Putout`转换，所以不需要再次遍历树。

这个`API`不该进来的🌴公共空间，反正它已经在`[eslint-plugin-putout](https://github.com/coderaiser/putout/tree/master/packages/eslint-plugin-putout)`到[测试插件](https://github.com/coderaiser/putout/blob/master/packages/eslint-plugin-putout/test/test-lint.mjs#L24-L28)中使用了，为什么不呢:)？不管怎样，它的签名从一开始就没变过。

# 让我们测试一下`ESLint`

![](img/169062d50cb66c00f3f4882b961a55f7.png)

> “宝宝整天看东西不眨眼；那是因为他的眼睛没有聚焦在任何特定的物体上。他不知道自己要去哪里，也不知道自己在做什么。他将自己融入周围的环境中，并随着环境移动。这些是心理卫生的原则。”
> ――庄子

# 测试有什么问题？

当你想测试`ESLint`规则时，你[可以](https://eslint.org/docs/developer-guide/unit-tests):

但是它很吵，而且编写测试的方式很奇怪🤔。当你有很多**有效**和**无效**的情况时，测试就变得看起来杂乱无章。同样`only`在事情开始时并不存在，即使它存在，也只是看起来很奇怪，更像是临时的。

# 我们来测试一下！

你可以用最简单的方法测试`ESLint`插件，使用 [@putout/test](https://github.com/coderaiser/putout/tree/v24.4.0/packages/test#eslint-api) 。

它是基于惊人的 [TAP](https://testanything.org/) 为基础的测试跑步者📼它延续了多语言测试的悠久历史，始于 1987 年。

> TAP 最初是作为 Perl 测试工具的一部分出现的，但是现在已经有了 C、C++、Python、PHP、Perl、Java、JavaScript、Go、Rust 等语言的实现。消费者和生产者不必用同一种语言编写就可以进行互操作。
> 
> [https://testanything.org/](https://testanything.org/)

创建测试所需的一切:

和`process`:

它的工作方式类似于[变换](https://github.com/coderaiser/putout/blob/master/packages/test/README.md#transformfilename--output-plugins)的方式:

*   ✅读`operator-linebreak.js`；
*   ✅改造了它；
*   ✅检查变换后的值是否等于`operator-linebreak-fix.js`；

当您想要传递选项时，请使用:

当您想要比较找到的位置时，请使用:

今天就到这里:)！祝你林挺愉快😏！

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***