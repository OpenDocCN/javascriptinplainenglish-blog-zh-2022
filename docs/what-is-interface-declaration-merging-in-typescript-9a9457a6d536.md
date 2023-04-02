# 什么是 TypeScript 中的接口声明合并？

> 原文：<https://javascript.plainenglish.io/what-is-interface-declaration-merging-in-typescript-9a9457a6d536?source=collection_archive---------3----------------------->

![](img/b6371067d3de358761ddc07b045fb0d3.png)

Photo by [Richard Horvath](https://unsplash.com/es/@orwhat?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/abstract?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

你可能会发现自己需要更新一个已经存在的**界面；然而**，这伴随着在其他地方打破它的用法，所以你怎么做？

这正是我们今天文章要回答的问题！

*文章最初发表于* [***此处***](https://upmostly.com/typescript/what-is-interface-declaration-merging-in-typescript) *。*

# 介绍

如果你还不熟悉**接口**的概念或者它们在 TypeScript 中是什么，一定要先看看 [**这篇**](https://upmostly.com/tutorials/what-are-interfaces-in-typescript) 文章，因为**接口声明合并**直接链接到它们。

否则，我们将继续文章的其余部分。

# 接口声明合并指的是什么？

处理文章开头提到的问题的最好方法是通过 **IDF** 或**接口声明合并**。

**接口声明合并**允许我们做的是，每当我们有两个同名的**接口**时，TypeScript 编译器会尝试将这两个接口的属性合并到一个它们共享名称的接口中。

TypeScript 允许合并多种类型，如**作为接口**、**枚举**、**命名空间**等。我们不能合并的一个显著例子是**类**。为此，我们将需要使用一个叫做 **Mixins** 的东西(这将在以后的一篇关于 [**直到**](https://upmostly.com/) 的文章中讨论)。

# 接口声明合并的示例

我们将通过代码示例尝试涵盖所有可能的合并情况:

```
interface Car {
  model: string;
  engineSize: number;
}

interface Car {
  manufacturer: string;
}

interface Car {
  color: string;
}

const car: Car = {
  color: 'red',
  engineSize: 1968,
  manufacturer: 'BMW',
  model: 'M4',
  numSeats: 4, // `numSeats` property is not specified
};
```

因为所有声明的接口共享相同的名称，所以它们将被合并到同一个名称下，同时共享集合属性。

同样，具有相同名称的所有属性应该是相同的类型。否则，将会引发编译错误，如下例所示:

```
interface Car {
  model: string;
  engineSize: number;
}

interface Car {
  manufacturer: string;
}

interface Car {
  color: string;
  numSeats: string;
}

interface Car {
  numSeats: number; // Error: Subsequent property declarations must have the same type.  Property 'numSeats' must be of type 'string', but here has type 'number'.ts(2717)
}

const car: Car = {
  color: 'red',
  engineSize: 1968,
  manufacturer: 'BMW',
  model: 'M4',
  numSeats: 4,
};
```

现在我们来看看具有相同属性名称的**接口**，其类型是函数:

```
interface Car {
  model: string;
  engineSize: number;
  manufacturer: string;
  color: string;
}

interface Car {
  start(param: string);
}

interface Car {
  start(param: number);
}

const bmw: Car = {
  model: 'M4',
  manufacturer: 'BMW',
  engineSize: 2993,
  color: 'white',
  start: (param) => param,
};

bmw.start(2) // `start(param: number)` will be used

bmw.start('3') // `start(param: string)` will be used
```

当合并包含具有相同签名的函数的接口时，最后声明的接口中的函数出现在合并接口的顶部，而第一个接口中声明的函数出现在下面:

```
interface Car {
  start(param: string);
}

interface Car {
  start(param: any);
}

interface Car {
  start(param: number);
  start(param: boolean);
}

// This is how the final merged interface looks like
interface Car {
  // functions in the last interface appear at the top
  start(param: number);
  start(param: boolean);

  // function in the middle interface appears next
  start(param: any): number;

  // function in the first interface appears last
  start(param: string): string;
}
```

原因是后来声明的接口比最初声明的接口优先级高。

如果我们考虑上面的例子，`start(param: string)`将永远不会被调用，因为在最终合并的`Car`接口中，start(param: any): number 方法声明在 start(param: string): string 方法声明之前，并且由于`any`可以代表任何类型，所以即使将`string`作为参数传递，它也会被调用。

除了同名函数参数有一个[字符串文字](https://www.digitalocean.com/community/tutorials/typescript-string-literal-types)作为**类型**的情况之外，所有接口都是如此。它遵循上述相同的顺序，但是字符串类型的函数被赋予更高的优先级，因此，通过**声明合并**，出现在顶部。

如上所述，后面接口中的字符串文字将出现在初始接口之前。

# 摘要

我希望你喜欢这篇文章，并更好地理解什么是**接口声明合并**，何时使用它会有帮助，更重要的是，我们将如何在我们已经存在的**接口**中使用它。

还要注意的是，在 React 内部使用 TypeScript 时，**接口**非常方便；您可以在这里查看一篇文章，该文章强调了使用 TypeScript 创建一个新的 React 项目，甚至是将 TypeScript 添加到一个已经存在的 React 项目中。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***