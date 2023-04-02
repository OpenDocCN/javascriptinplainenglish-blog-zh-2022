# 自举与顺风响应之战

> 原文：<https://javascript.plainenglish.io/the-bootstrap-vs-tailwind-responsiveness-battle-6a9b37a24592?source=collection_archive---------8----------------------->

## 为什么顺风会赢

![](img/58f8c3a14f3e759608b5875ed964c89b.png)

这两个库在前端社区中都被大量使用。据说顺风更可定制，而自举被认为更精简，因此学习起来更快。

今天我们来看看这两个库的响应特性。我们都知道自己写媒体查询的麻烦，即使使用 SCSS mixins 会加快速度。简单地向 DOM 元素添加一个类可以节省大量时间。但是哪个库更擅长提供这个特性呢？

# 断点

首先，当我们谈论响应行为时，它总是指某些断点。这是因为布局经常从某个设备宽度开始改变。

断点是某些视口宽度，通常与设备类型相关联。两个库都用这些快捷方式引用这些断点:

sm —小型

md —中等

lg —大型

xl —特大号

库之间的默认断点宽度(以像素为单位)不同。例如，Bootstrap 中的大断点位于 992px，而 Tailwind 中的大断点位于 1024px。但是，您可以在两个库中配置断点。

# 移动优先

这两个库都是移动优先的:通常应用一个 CSS 类，然后为特定的断点添加该类的修改版本。这就是为什么您找不到正在使用的 xs 断点。

# 引导中的响应类

Bootstrap 允许您将断点修饰符应用于所有 CSS 类的子集，这也是响应性是常见用例的部分。换句话说，支持针对不同设备呈现不同样式的 CSS 样式。

## 列

在 bootstrap 中，可以通过在类中添加断点来使用响应列类:

`.col-{breakpoint}-{value}`为`1 - 12`，`auto`

```
<div class="row"> 
    <div class="col-6 col-lg-3">col 1</div>
    <div class="col-6 col-lg-3">col 2</div>
    <div class="col-6 col-lg-3">col 3</div>
    <div class="col-6 col-lg-3">col 4</div>
</div>
```

Bootstrap 将总宽度分为 12 部分，因此如果使用 col-6，这意味着该列应该占总宽度的一半(6/12)。从断点大开始，它占总宽度的四分之一(3/12)。容器元素需要类`row`。这会将容器设置为 display: flex，并应用一些其他 CSS 属性。更多详情请点击此处:

[](https://getbootstrap.com/docs/5.2/layout/grid/) [## 网格系统

### Bootstrap 的网格系统使用一系列容器、行和列来布局和对齐内容。它是由…

getbootstrap.com](https://getbootstrap.com/docs/5.2/layout/grid/) 

## 显示

还可以将断点标识符与显示类一起使用。

`.d-{breakpoint}-{value}`为`sm`、`md`、`lg`、`xl`、`xxl`

```
<div class="d-inline-block d-lg-flex">I am responsive</div>
```

div 显示为内联块，从断点开始显示为伸缩框。

[](https://getbootstrap.com/docs/5.2/utilities/display/) [## 显示属性

### 使用我们的响应显示实用程序类来更改 display 属性的值。我们特意只支持…

getbootstrap.com](https://getbootstrap.com/docs/5.2/utilities/display/) 

## 边距和填充

对于较大的设备，通常会增加边距和填充。

`.{property}{sides}-{breakpoint}-{size}`为`sm`、`md`、`lg`、`xl`和`xxl`

在这里，我将{sides}去掉，这意味着该属性(例如填充)将应用于所有边。

```
<div class="m-1 m-lg-4">I am responsive</div>
<div class="p-1 p-lg-4">I am responsive</div>
```

这里，边距和填充被设置为间隔 1，等于 4px，直到断点变大，在断点变大时，它被设置为间隔 4，等于 16px。

[](https://getbootstrap.com/docs/5.2/utilities/spacing/) [## 间隔

### 用速记类将响应友好的边距或填充值分配给元素或其边的子集…

getbootstrap.com](https://getbootstrap.com/docs/5.2/utilities/spacing/) 

## 文本

文本对齐方式:

`.text-{breakpoint}-{value}`为开始、中心、结束

```
<p class="text-start text-lg-end">Lorem ipsum</p>
```

这里，文本首先接收 CSS 规则:`text-align: left`并从大断点开始`text-align: right`。

[](https://getbootstrap.com/docs/5.2/utilities/text/) [## 文本

### 使用文本对齐类轻松地将文本重新对齐到组件。对于开始、结束和中心对齐，响应类…

getbootstrap.com](https://getbootstrap.com/docs/5.2/utilities/text/) 

# 顺风

使用 Tailwind，可以将断点修饰符应用于它的所有类。这也包括类，它们不是响应的典型目标。

想从断点大处开始将文本显示为粗体并加下划线吗？没问题。

您只需在类前面加上断点修饰符:

`.{breakpoint}:{value}`

```
<h1 class="lg:font-bold lg:underline">Tailwind Responsiveness</h1>
```

这只是一个例子。Tailwind 有数百个实用程序类，所有这些类都可以依赖断点使用。如果你问我，我会觉得这很神奇。自写的媒体查询基本没什么用了。

我想提到的另一个例子是列，因为这是我在 Bootstrap 中使用最多的特性。这将呈现与前面的引导示例中相同的列分布:

```
<div class="columns-2 lg:columns-4">
    <div>col 1</div>
    <div>col 2</div>
    <div>col 3</div>
    <div>col 4</div>
</div>
```

在 Tailwind 中，您可以直接告诉父类您想要多少列，而不是按 12 列的比例给各个类一个宽度:就像在 Bootstrap 示例中一样，2 列是为小视口渲染的，4 列从大视口开始。

[](https://tailwindcss.com/docs/responsive-design) [## 响应式设计——顺风 CSS

### Tailwind 中的每个实用程序类都可以在不同的断点处有条件地应用，这使它变得轻而易举…

tailwindcss.com](https://tailwindcss.com/docs/responsive-design) 

# 谁赢了？

这两个库都可以通过提供响应类来加速前端开发。由于断点修饰符可以应用于任何 Tailwind CSS 类，因此 Tailwind 提供了更具响应性的功能。然而，对于许多用例来说，Bootstrap 的功能就是所需要的全部。

# 哪个适合你？

这两个库在支持响应方面都做得很好，选择取决于项目需求。注意:选择其中一个库，不要两个都用。这些库有几个相同的 CSS 类，这将导致冲突。除此之外，这也让开发者感到困惑。

要决定使用哪一个，一个好方法是使用 CDN 链接进行简单快速的设置。您不需要安装 npm 软件包时获得的全部功能，但它应该足以确定您更喜欢哪一个。

感谢您的阅读！如果我忘记了任何相关的信息，请在评论中告诉我，我很乐意补充。web 开发内容请关注我。

## 更多资源

顺风设置文件[https://tailwindcss.com/docs/installation](https://tailwindcss.com/docs/installation)

引导设置文档[https://get bootstrap . com/docs/5.2/getting-started/introduction/](https://getbootstrap.com/docs/5.2/getting-started/introduction/)

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查出* [***电路***](https://circuit.ooo/) ***。****