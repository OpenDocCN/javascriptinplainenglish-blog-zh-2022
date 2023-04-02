# 魔弦还是常数？

> 原文：<https://javascript.plainenglish.io/magic-strings-or-constants-a0fdcdda197c?source=collection_archive---------2----------------------->

![](img/cb3b2798d3b8cb455426985d3132599f.png)

Photo by [Steve Johnson](https://unsplash.com/@steve_j?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

神奇字符串(或数字)的定义非常清楚——它是一个**硬编码的值，决定了你的程序如何工作**。
使用起来方便快捷；不需要额外的代码或导入，如果您知道代码库，您就知道使用什么值。

*那又怎么了？为什么还要考虑替代方案呢？*

人们可以说魔术字符串是一种不好的实践或者反模式。让我们假设这是真的，但问题仍然是“为什么？”。我希望我的解释、论据和例子能帮助你做出决定。我不认为`const`总是任何规模的任何项目的解决方案，但是我想分享一些使用它们的理由。

**Identity**
Magic string 仅仅是一个在编写代码时对代码作者有意义的词(我保证，几个月后你将不得不花额外的一分钟去理解它的意思)。当直接作为一个神奇的字符串使用时，value 可能会与其他东西混淆，尤其是在大规模应用程序中，而 const 更清楚地表明它是什么。

例如:`'personal'`对`const USER_PROFILE_TYPE = 'personal';`

而修正这一点，如果同一个词在不同的成分中代表不同的东西，很容易被误替换。

使用幻数会带来额外的缺点。虽然单词可以不言自明(至少在某种程度上)，但数字很难，偶然替换它们甚至更容易。

例如:`'1024'`对`const MAX_FILE_SIZE = '1024';`

正因为如此，我建议在你的代码中避免使用魔法，但这还不是全部…

**上下文和代码组织**
谈到常量，人们可能会想到一些非常多余的东西——给`const`分配一个同名的字符串，更像这样:

```
const small = 'small';
const medium = 'medium';
const large = 'large';
```

没错，这没什么意义。但是，如果您有多个属于一起或共享上下文的值，您有以下选择:

```
const SIZES = {
  small: 'small';
  medium: 'medium';
  large: 'large';
}
```

我们可以更进一步，组织我们的代码以进一步提高可读性:

```
const COLORS = {
  primary: 'FF9933';
  secondary: '138808';
  tertiary: '000080';
}

const GRAYSCALE = {
  white: 'FFFFFF';
  ink: '333';
}

const COLOR_PALETTE = {
  COLORS,
  GRAYSCALE,
}
```

**重用** 这一点值得商榷。当然你不会重用一个神奇的字符串，但是你也不会总是重用常量。尽管如此，为了保持一致性，在文件顶部定义`const`还是很方便的。

当然，当你需要在多个地方使用同一个值时，甚至在同一个文件中，你应该使用`const`。

最简单的例子就是当你使用一个组件库的时候。当你用它们做积木的时候，你会用很多。在替换所选选项的值时，有很多机会出现输入错误，以及大量额外的工作。

以下是如何避免前者并将后者最小化:

```
const COMPONENT_SIZE = {
  sm: 'small'
  md: 'medium'
};

<ui-button
  :size="COMPONENT_SIZE.sm"
/>

<ui-button
  :size="COMPONENT_SIZE.md"
/>
```

**事实的来源** 如果您决定在应用程序的多个域之间共享上下文，它会提供可用值的“事实的来源”。
当你需要改变全局的值时，你需要做的就是在一个地方更新它，而不是一个接一个地在你的代码中做所有的魔术，再次冒着出错的风险。

**Intellisense** 琐碎，但相当有用。拥有常量可以让你总是从有效的选项中选择，而不是冒打错字的风险。

总结一下，是的，我建议我的同事使用常数，是的，问题相对简单，但是我发现自己经常解释它们的好处。如果以上都不能说明问题，那么我的最后一个观点就是组织代码，让你可以跟踪选项。

编码快乐！

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

***有兴趣缩放你的软件启动*** *？检查出* [***电路***](https://circuit.ooo/?utm=publication-post-cta) *。*