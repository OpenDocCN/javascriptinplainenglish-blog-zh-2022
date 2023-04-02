# Sass:专业级 CSS 扩展语言

> 原文：<https://javascript.plainenglish.io/sass-professional-grade-css-extension-language-e75765e01660?source=collection_archive---------19----------------------->

## 2 分钟学会最强大的 CSS 扩展语言。

Sass 是世界上最成熟、最稳定、最强大的专业级 CSS 扩展语言。

![](img/fb6a9e3cb3dbfc7e276c737308d49f7f.png)

Image from the [official site](https://sass-lang.com/) of Sass

CSS 预处理器，**S**yntacally**A**we some**S**style**S**sheet(Sass)是 CSS 的扩展。当样式表变得越来越大、越来越复杂、越来越难维护时，Sass 可以帮助减少 CSS 的重复并节省时间。浏览器不理解 Sass 代码。因此，在将 Sass 代码发送到浏览器之前，Sass 预处理器会将其转换为标准 CSS，这个过程称为***trans pilling***。

让我们考虑一个例子，你在一个 CSS 文件中使用相同的颜色 20 次。现在，如果一个客户想要不同的颜色，那么在使用 CSS 的情况下，你需要改变它 20 次。Sass 通过引入变量、嵌套规则、混合、导入、继承、内置函数等许多特性来解决这个问题。为了在我们的项目中实现 Sass，我们需要首先安装它。你可以从[这里](http://sass-lang.com/install)安装。

Sass 有两种语法，SCSS 语法(。scss)和 SASS 语法(。sass)。主要区别在于 sass 使用缩进而不是花括号来嵌套语句，并且使用换行符而不是分号来分隔语句。

## 语法示例:

```
//SCSS Syntax
$main-color: #a2b9bc;
body {
  color: $main-color;
}//SASS Syntax
$main-color: #a2b9bc
body
  color: $main-color
```

# Sass 变量

Sass 提供了变量来存储我们以后可以重用的信息。此外，我们可以通过改变单个变量的值来改变信息。Sass 变量的语法是:`$*variablename*: *value*;`

# Sass 嵌套规则和属性

与标准 CSS 相比，Sass 允许以更简单、更干净的方式嵌套 CSS 选择器。请参见下面的示例:

```
$main-color: #a2b9bc;
nav {
  ul {
    margin: 0;
    padding: 0;
  }
  li {
    color: $main-color;
  }
}
```

此外，在 CSS 中，一些属性有相同的前缀。例如，字体系列、字体大小和字体粗细。在 Sass 中，您可以将它们编写为嵌套属性，如下所示:

```
font: {
  family: Helvetica, sans-serif;
  size: 20px;
  weight: bold;
}
```

# Sass 导入

像 CSS 一样，Sass 也支持导入功能，允许我们将一个文件的内容包含在另一个文件中。我们可以根据需要包含任意多的文件。请看下面的例子来阐明这个概念:

```
// File 1 named ***first.scss*** body {
  margin: 0;
  padding: 0;
}// File 2 named ***main.scss*** @import "first"; // file extension does not require.

body {
  font-family: Helvetica, sans-serif;
  font-size: 20px;
}
```

# Sass Mixin 和 Include

Sass Mixin 使 CSS 代码能够被重用，Sass Include 允许我们使用或包含该 Mixin。参见下面的例子来理解 ***mixin*** 和 ***包含*** 的语法和用例。

```
***// Here, we created a mixin.***
@mixin special-text {
  color: #a2b9bc;
  font-size: 30px;
  font-weight: bold;
}
.main-text {
 ** *//Here, we included the mixin.***
  @include special-text;
  background-color: blue;
}
```

我们也可以将变量作为参数传递给 mixin。然后，我们可以在包含 mixin 时设置参数的值。请参见下面的示例:

```
***// Here, we created a mixin with two arguments.*** @mixin border-prop($color, $width) {
  border: $width solid $color;
}

.mainBody {
  // ***Here, we included the mixin, and passed the values.***
  @include border-prop(red, 2px);  
}
```

# Sass 扩展/继承

Sass 扩展允许我们从一个选择器到另一个选择器继承属性。Sass 提供了另一个与*扩展*密切相关的特性，称为**占位符**类(以%开头)。*占位符类*是一种特殊类型的类，它只在被扩展时才打印，可以帮助你保持编译后的 CSS 整洁。然而，你总是可以使用一个带有 Sass 扩展特性的普通 CSS 类。参见下面的例子来学习 Sass 的 ***扩展*** 特性带有一个*类以及一个 ***常规*** 类。*

```
****// This is a regular CSS class.***
.basic-class  {
  cursor: pointer;
}***// This CSS will print in compiled CSS because it is extended.***
%class-in-use {
  border: 1px solid #ccc;
  color: #ffff;
}

***// This CSS won't print because it is never extended.***%class-never-used {
  display: flex;
  flex-wrap: wrap;
}

.main-body {
  ***//Here, we extended %class-in-use***
  @extend %class-in-use;
  ***//Here, we extended .******basic-class***
  @extend .basic-class;
  background-color: blue;
}*
```

# *结论*

*这篇文章的目的是学习语法上令人敬畏的样式表 的基础知识。我还给出了 Sass 中包含的所有特性的单独示例。您还可以从 Sass 的官方网站了解 Sass 提供的更多高级特性和功能。我希望你喜欢跟我学顶嘴。请跟随我学习更多像这样有趣的东西，并保持更新。*

*[](https://medium.com/@kardaniyagnik/membership) [## 通过我的推荐链接加入 Medium-Yagnik Kardani

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

medium.com](https://medium.com/@kardaniyagnik/membership) [](https://www.buymeacoffee.com/kardaniyagnik) [## Yagnik Kardani 正在创建帮助他人成长的技术学习材料。

### 你好👋，我是一名媒体方面的技术作家。我喜欢学习并帮助他人在软件开发和云计算方面成长…

www.buymeacoffee.com](https://www.buymeacoffee.com/kardaniyagnik) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。**