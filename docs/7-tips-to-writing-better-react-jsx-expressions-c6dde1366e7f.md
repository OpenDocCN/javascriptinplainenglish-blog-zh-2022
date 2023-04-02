# 写更好的反应 JSX 表达的 7 个技巧

> 原文：<https://javascript.plainenglish.io/7-tips-to-writing-better-react-jsx-expressions-c6dde1366e7f?source=collection_archive---------4----------------------->

## 使用 React JSX 创建更好的 JSX 表达式并提高您创建动态网页的能力的提示和技巧。

![](img/90691c8831e2db33ba69f203c59444a9.png)

Photo by [Windows](https://unsplash.com/@windows?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

编写 JSX 表达式是使用 React 创建快速渲染的高效代码的基础部分，能够编写可以处理各种元素的简明 JSX 表达式是一项重要的技能。

在这篇文章中，我将分享一些写更好的 JSX 代码的技巧(如果你感兴趣，我在最近的一篇文章中讲述了如何编写和渲染 JSX 表达式的基础知识)。

# 1.添加类属性

通常，JSX 属性的添加方式与 HTML 属性相同。属性名被设置为等于它在开始标记中的值。但是有一个例外，那就是 class 属性。

单词 class 在 JavaScript 中是保留的，因此编写`class=”class_name"`将不起作用。相反，属性需要写成`className`。当渲染 JSX 时，这将自动转换为类，并且该类的所有 CSS 样式都将应用于它。

```
const = <h1 className="title">Welcome to our page</h1>;
```

# 2.自动结束标签

在当前的 HTML 语法中，当使用自结束标记时，标记末尾的反斜杠是可选的。

然而，反斜杠在 JSX 不是可选的。如果没有它，编译脚本时将会出错。

```
<img src="my_photo.jpg"> //This will work in HTML but not JSX<img src="my_photo.jpg"/> //This is the syntax needed in JSX
```

# 3.在 JSX 和 Javascript 之间切换

JSW 表达式的一个强大之处是它们可以在其中包含 JavaScript。这允许交互式和动态的网页内容。

为了让 Javascript 在 JSX 表达式中工作，你需要使用花括号。然后，括号中的内容被评估为 Javascript 表达式。

```
<h1>2 +3</h1> // Returns 2 + 3
<h1>{2 + 3}</h1> //Returns 5
```

可以像在标准 JavaScript 表达式中一样访问和使用主 JavaScript 文件中的变量。

```
const name = 'Stef';

const welcome = <p>Hello {name}!</p>;
```

# 4.添加事件侦听器

扩展一下 JavaScript 的这种用法，可以用来创建动态内容的一种技术是将事件监听器合并到 JSX 表达式中。

例如，将“点击”属性添加到结合了 JavaScript 函数的照片:

```
<img onClick={myFunc} />
```

要获得可添加事件的完整列表，请查看 [React 事件文档](https://reactjs.org/docs/events.html#supported-events)。

# 5.在 JSX 使用条件句

JSX 还允许使用某些条件，根据用户的输入或定义的变量向用户提供定制内容。

如果您想在条件为真时只显示某些内容，可以使用`&&`操作符。

以下面的 JSX 表达式为例，在登录时，用户可能会被询问他们的年龄，这个输入被保存为一个变量。当用户想要查看饮料列表时，可以调用 JSX 表达式。

表达式会自动呈现单词 water。那么由于年龄变量大于 21，它也将呈现葡萄酒选项。如果用户的年龄在 21 岁以下，则语句的这一部分将不会完成。

```
let age = 23;
let drinkList = (
      <ul>
        <li>Water</li>
        { age > 21 && <li>Wine</li>}
      </ul>
          );
```

# 6.高效的列表制作

要创建一个更长的 JSX 元素列表，可以使用`.map()`而不是写出一个完整的列表。这样做的好处是可以对 JavaScript 文件中的数组进行操作，然后修改后的数组会在准备就绪时呈现给页面。

```
const menuItems = ['Tomato Soup', 'Chicken Salad', 'Pizza'];

const listItems = menuItems.map(item => <li>{item}</li>);

<ul>{listItems}</ul>
```

# 7.创建有序列表

使用 JSX 创建列表时，标准做法是添加关键属性。这可以确保在渲染过程中 React 不会打乱列表顺序。

您应该确保使用具有唯一值的`key`属性，如下例所示。

```
<ul>
  <li key="li-01">Example1</li>
  <li key="li-02">Example2</li>
  <li key="li-03">Example3</li>
</ul>
```

有关如何有效使用键的更多信息，您应该查看关于该主题的 [React 键文档](https://reactjs.org/docs/lists-and-keys.html)。

# 摘要

这些只是一些提示，希望能让你释放 JSX 表达式给 web 开发项目带来的更多力量。虽然每个技巧都包含一些相对简单的内容，但它们都可能对动态网页的开发产生重大影响。

如果你有其他任何你认为应该列在这个清单上的技巧和诀窍，请告诉我——我很有兴趣听听它们！

***如果你喜欢这篇文章并想阅读更多，一定要看看我的类似文章。***

***考虑成为一名媒介会员，以获得无限接触最佳创意和作家的机会。*** [***如果你通过这个链接加入 Medium，我会从你的费用中收取很少的一部分——而且不会花你任何额外的费用！提前感谢。***](https://medium.com/@simply_stef/membership)

***感谢阅读！***

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*