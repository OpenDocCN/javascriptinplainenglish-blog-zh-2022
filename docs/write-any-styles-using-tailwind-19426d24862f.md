# 使用顺风书写任何样式

> 原文：<https://javascript.plainenglish.io/write-any-styles-using-tailwind-19426d24862f?source=collection_archive---------8----------------------->

## 你能用 CSS 编写的任何东西都可以用 Tailwind 通过一些巧妙的语法技巧来编写。

![](img/68f6523c7f8c9870154b2b5b3ec963b5.png)

Photo by [KOBU Agency](https://unsplash.com/@kobuagency?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Tailwind 是一个使用类名编写简写内联 CSS 的不可思议的工具。虽然由于顺风的设计方式，它有时会感到受约束。然而，事实是，使用一些巧妙的语法技巧，任何可以用 CSS 编写的东西都可以用 Tailwind 编写。

# **设置**

本文假设在尝试这些技术之前，您的项目中已经安装了 Tailwind。如果你的项目中还没有 Tailwind，那么去看看 [Tailwind 文档](https://tailwindcss.com/docs/installation)并找到关于你的特定框架的说明。

此外，如果你使用的是 VSCode，你还可以安装[官方的 Tailwind 扩展](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss)来获得更好的智能感知。

# **任意属性**

假设我想要一个宽度为 200 像素的单个元素。我可以在我的 Tailwind 配置中添加一个自定义类，但是如果每次我需要一个奇怪的特定属性时都这样做，我会得到一个非常混乱的设置。相反，我可以使用 Tailwind 的任意属性语法为我的元素提供任何我喜欢的宽度值。

使用 width 实用程序前缀，后跟我的 CSS 属性，用括号括起来，tailwind 将生成一个具有适当值的类。

```
<div class="w-[200px]"></div>
```

您仍然可以使用任何修饰符，如`md:`或`hover:`。

```
<div class="hover:w-[210px]"></div>
```

# **任意变体**

使用任意变量，你可以定制一个 Tailwind 类的选择器。使用`&`前缀，后跟一个 CSS 选择器。若要表示空格，请使用下划线。例如，我们可以用它来选择一个 div 的所有子`p`元素，并对每个元素应用边距。

```
<div class="[&_p]:my-4">
  <p>
    Hello world!
  </p>
  <p>
    Lorem ipsum...
  </p>
</div>
```

另一个例子，我们可以选择元素的第一个子元素，并应用背景颜色。

```
<div class="[&first-child]:bg-gray-200">
  <p>
    This element has a gray background
  </p>
  <p>
    This element does not.
  <p>
</div>
```

# **编写完全任意的 CSS**

所以，下一个有点奇怪，但偶尔会有用。通过将您的类放在括号中，您可以编写一个普通的 CSS 键/值对。空格仍然应该用下划线代替，但这是唯一的警告。例如，这允许我为我的 div 编写一个表示背景图像的类。

```
<div class="w-48 h-48 bg-cover [background-image:url('my-image.png')]"></div>
```

你可能会问这样做的好处是什么，尤其是考虑到下划线语法，这比仅仅编写简单的内联 CSS 更值得考虑。事实是，这允许一些用普通内联 CSS 做不到的漂亮技巧。

使用这种语法，您仍然可以应用像`hover:`、`focus:`或`dark:`这样的修饰语。因此，任何需要存在的媒体查询或元素状态都可以在类名中定义。这在使用内联样式时是不可能的，所以这在编写更复杂的 UI 组件时是一个巨大的优势。

```
<div class="w-48 h-48 bg-cover hover:[background-image:url('my-image.png')]"></div>
```

# **结论**

Tailwind 无疑是一个有争议的实用框架，但毫无疑问，它已经在许多项目中取得了巨大的成功，并帮助带来了一种编写 CSS 的新方法。感谢它背后令人惊叹的团队的许多更新，我们推动自己走向更好的开发者体验。

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*