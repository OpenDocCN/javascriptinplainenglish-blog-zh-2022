# 打字稿的基础，难度逐渐增加

> 原文：<https://javascript.plainenglish.io/the-fundamentals-of-typescript-in-increasing-levels-of-difficulty-c54bab69fbb9?source=collection_archive---------11----------------------->

![](img/05db14bcadd17daafb62c6915466e932.png)

Source: Wikimedia Commons

当 TypeScript 在近十年前首次发布时，几乎所有使用它的开发人员都是从 JavaScript 过渡而来的。即使在今天，大多数使用 TypeScript 的开发人员都是在 JavaScript 之后或在 JavaScript 环境中学习这种语言的。毕竟，这是自然的方法。

但是这种方法有一个关键问题:JavaScript 中的类型不同于 TypeScript 中的类型。当您在 JavaScript 环境中学习 TypeScript 时，很难对类型的基础有很强的直觉。

在本文中，我们将更仔细地研究 TypeScript，从基础开始，并有意识地向更健壮的设计模式前进。在每一步，我们将深入研究基础知识，以帮助培养对更复杂类型的直觉。

我写这篇文章的目的是让那些从未使用过 TypeScript 的人也能接触到它(有耐心，可能还会搜索一下),同时让那些每天使用它的人也能感受到它的趣味性和快节奏。

# 基元

您可能不会对如何声明类型化变量感到惊讶:

```
const query: string;
```

但是很容易忘记即使是最简单的 TypeScript 语句实际上是如何在幕后工作的。

不直接解释 TypeScript。相反，它被转换成 JavaScript，在此过程中所有类型注释都被删除。在执行时，就解释器所知，变量没有类型——只有它们的值有。保存数字的变量可以被设置为保存一个字符串，或者一个函数，或者什么都不保存。在运行时，你所有的辛苦工作都被扔出了窗外。

这给我们带来了 TypeScript 最基本的规则之一:**类型永远不会影响代码的执行，JavaScript 中的运行时类型与 TypeScript 中的类型有着本质的区别。**如果不完全吸收这一原则，你就无法开发或调试 TypeScript 应用程序。

因此，TypeScript 开发的最大挑战之一是理解何时可以在运行时确定变量的类型，并知道该类型的精度。没有这些信息，您就不能分配正确的类型，或者根本不能分配任何类型。

# 并集和交集

**TypeScript 中的类型只不过是可能值的集合**。例如，`boolean`类型是包含值`true`和`false`的集合。

一些类型代表(实际上)无限大的集合，比如`string`和`number`。

而且甚至还有一种代表空集的类型:`never`。没有什么可以被指定为`never`类型。我们会深入探讨你为什么想这么做。

因为类型是集合，我们可以考虑使用两个基本的集合操作来操作类型:并集和交集。两个集合的**并**是存在于*或*集合中的所有元素的集合。两个集合的**交集**是两个集合*中所有元素的集合。*

我们在 TypeScript 中用`|`表示并集，用`&`表示交集。让我们看一些例子。

假设我们这样定义一个类型:

```
type DiceValues = 1 | 2 | 3 | 4 | 5 | 6;
```

记住:类型只是一组值。类型`1`是单个值的集合:数字`1`。(原语既可以是类型，也可以是值；不要让这个迷惑你。)

因此，`1 | 2`是类型`1`和`2`的并集，而类型`DiceValues`代表了在 6 面骰子上可能出现的所有值。

```
type EvenValues = 2 | 4 | 6;
type OddValues  = 1 | 3 | 5;
type PrimeValues = 2 | 3 | 5;
```

现在我们有了这些类型，我们可以对它们执行有趣的操作:

```
type A = EvenValues | OddValues
```

类型`A`相当于`DiceValues`。

```
type B = EvenValues & OddValues
```

一个数不能既是偶数又是奇数。因此，类型`B`相当于`never`。

```
type C = OddValues & PrimeValues;
```

类型`C`相当于`3 | 5`。

# 并集和交集-与对象

对象是 JavaScript 的基础。对象只不过是键到值的映射。当所有的键和值都是同一类型时，我们可以使用`Record`实用程序类型来表示:

```
type WordsToLengths = Record<string, number>;const wordsToLengths: WordsToLengths = {
  "ruler": 5,
  "file": 4,
  "": 0,
}
```

很简单。但是 JavaScript 中的对象并不总是像字典一样结构化。键可以是字符串或数字，值可以是任何类型——键和值的类型甚至可以在同一个对象中不一致，就像在 JSON 对象中一样。

要定义更复杂对象的类型，我们可以这样做:

```
type User = {
  id: number;
  email: string;
  name: string;
  hasSignedIn: boolean;
}type Guest = {
  name: string;
  ip: string;
}
```

同样，这些类型是不言自明的。但是`|`和`&`操作符如何处理这些类型呢？

记住类型`User`和`Guest`只是表示满足它们各自形状的所有可能值的集合。因此，`User | Guest`是满足任一形状的对象集合。具体来说，这意味着什么？

我们知道任何类型为`User | Guest`的值都必须有一个值为`string`的`name`属性。我们知道它可能有一个`ip`，也可能有一个`email`、`id`和`hasSignedIn`；这些情况中至少有一个必须是真的。

路口呢？嗯，`User & Guest`是同时满足*`User`形状和`Guest`形状的对象集合。您可以添加任何您想要的任意的、不相关的属性，只要您拥有由`User`和`Guest`指定的属性。例如:*

```
*const userAndGuest: User & Guest = {
  id: 5,
  name: "John",
  email: "john@doe.com",
  hasSignedIn: true,
  ip: "127.0.0.1",
  age: 80,
}*
```

*一般来说，当使用`|`和`&`操作符时，将类型视为集合，并将并集和交集视为对这些集合的操作。*

# *泛型和“extends”关键字*

*像大多数其他类型化语言一样，TypeScript 支持泛型。你可以认为泛型是类型的一个函数；将一种类型传递给另一种类型来创建新类型。*

*例如，我们可能有一个通用的`Action`类型:*

```
*type Action<PAYLOAD> = {
  name: string;
  payload: PAYLOAD;
}const setAge: Action<number> = {
  name: "setAge",
  payload: 5,
}*
```

*我们可以将泛型类型`PAYLOAD`约束为某种类型:*

```
*type Action<PAYLOAD extends number | string> = {
  name: string;
  payload: PAYLOAD;
}*
```

*现在，`"hello"`或`5`或`DiceValues`都是`PAYLOAD`的有效类型，因为`"hello”`扩展了`string`而`5`扩展了`number`。例如，`never`和`true`类型都没有扩展。*

*乍一看，这似乎违反直觉:为什么类型`"hello"`扩展了类型`string`？难道不应该反过来吗？*

*`extends`可以认为是一个“是一个”的关系:`"hello"`是一个`string`，`5`是一个`DiceValues`。但是我们知道所有的类型都是集合，所以`extends`关键字在集合论中一定有一些类比。这是什么？*

*如果类型`A`扩展了`B`，这意味着由类型`A`表示的所有可能值也在类型`B`中。这保证了我们可以对类型为`B`(在本例中为`number | string`)的值进行的任何操作也可以对传递给`Action`的泛型类型的值进行。*

*用集合的术语来说，这叫做子集。如果`A`是`B`的子集，则`A`扩展`B`。选择这个词是违反直觉的，但是将类型看作集合会使事情更容易推理。*

# *条件类型和提取*

*回想一下上面的`Action`定义:*

```
*type Action<PAYLOAD extends number | string> = {
  name: string;
  payload: PAYLOAD;
}*
```

*假设给了我们一个`const a: Action<any>`，我们想知道`a`的有效载荷类型。为了提取这个泛型类型，我们使用了一种叫做条件类型的东西。*

*上面，我们使用了`extends`关键字来约束泛型类型——现在，我们可以反过来，使用相同的关键字来检查类型是否满足约束:*

```
*type PayloadOfAction<A extends Action<any>> = 
    A extends Action<string> ? string : number;*
```

*这种类型就像一个函数:它接受一个`Action<P>`并返回`P`。*

*它之所以有效，只是因为我们知道`P`一定是`number | string`。我们检查一下`A extends Action<string>`；如果是，我们知道`P`一定是字符串，如果不是，一定是数字。*

*但是如果有两种以上的可能性呢？假设我们从`Action`类型中移除了通用约束:*

```
*type Action<PAYLOAD> = {
  name: string;
  payload: PAYLOAD;
}*
```

*现在，`PAYLOAD`可以是任何类型。如何用条件类型提取呢？*

*输入`infer`关键字。在条件类型内部，我们可以使用`infer`来要求 TypeScript 给出确切的泛型类型:*

```
*type PayloadOfAction<A extends Action<any>> = 
    A extends Action<infer P> ? P : never;*
```

*我们遇到了一个实际使用`never`类型的例子。`A`将*总是*扩展`Action<infer P>`，因为`infer`关键字可以推断任何类型。因此，`PayloadOfAction`将总是返回`Action`的确切有效载荷类型。*

*`infer`只能在条件类型中使用，所以即使这种构造看起来不自然，使用`never`是直接提取泛型类型的唯一方法。*

# *映射类型*

*从上面回忆我们的`Guest`式:*

```
*type Guest = {
  name: string;
  ip: string;
}*
```

*假设我们有一个对象将客人的 IP 映射到姓名:*

```
*const ipsToNames = {
  "127.0.0.1": "John",
  "124.70.8.54": "Susan",
  "1.1.1.1": "Alex",
}*
```

*如果我们想转换这个映射，使其将相同的 IP 映射到`Guest`而不是名称，该怎么办？转换后的地图将如下所示:*

```
*const transformedMap = {
  "127.0.0.1": {
    ip: "127.0.0.1",
    name: "John",
  },
  "124.70.8.54": {
    ip: "124.70.8.54",
    name: "Susan",
  },
  "1.1.1.1": {
    ip: "1.1.1.1",
    name: "Alex",
  },
}*
```

*如果没有严格的类型，我们很容易忘记包含一个 IP，或者添加一个额外的 IP，或者输入错误的 IP。我们希望在原始地图的基础上键入转换后的地图，以确保我们拥有完全相同的键:*

```
*type IPsToGuests<M extends Record<string, string>> = {
  [KEY in keyof M]: Guest
}*
```

*通用类型`M`是原图的类型，是一个`Record<string, string>`。*

*我们现在可以给`transformedMap`分配类型`IPsToGuests<typeof ipsToNames>`。这将确保转换后的贴图具有与原始贴图完全相同的键。*

*但是有一个问题。`IPsToGuests`只是约束新映射的*键*——对象的值必须是`Guest` s，但不一定是正确的 IP 或名称。例如，我们可以交换约翰和苏珊的来宾对象:*

```
*const transformedMap = {
  "127.0.0.1": {
    ip: "124.70.8.54",
    name: "Susan",
  },
  "124.70.8.54": {
    ip: "127.0.0.1",
    name: "John",
  },
  "1.1.1.1": {
    ip: "1.1.1.1",
    name: "Alex",
  },
}*
```

*我们希望确保每个`Guest`值都有相同的 IP 作为它的键，并且客人的名字是基于原始地图中相应的名字。*

*为此，我们首先使`Guest`成为泛型，因为我们需要对它的属性引入特定的约束:*

```
*type Guest<IP extends string, NAME extends string> = {
  ip: IP,
  name: NAME,
}*
```

*现在，我们可以改进我们对`IPsToGuests`的定义:*

```
*type IPsToGuests<M> = {
  [KEY in keyof M]: Guest<KEY, M[KEY]>
}*
```

*这告诉 TypeScript,`IP`类型应该匹配键，而`NAME`应该匹配原始映射中的相应值。*

*我们可以更进一步。假设我们想要生成一个类型`AllGuests`，它代表来自`ipsToNames`的所有可能的`Guest`类型:*

```
*type John = {
  ip: "127.0.0.1",
  name: "John",
}type Susan = {
  ip: "124.70.8.54",
  name: "Susan",
}type Alex = {
  ip: "1.1.1.1",
  name: "Alex",
}type AllGuests = John | Susan | Alex;*
```

*当然，我们希望能够基于我们最初的`ipsToNames`类型自动生成这个类型。*

*我们可以使用我们的`IPToGuests`类型来帮助我们。我们想要的是`IPsToGuests<M>`中所有*值*的联合。这很简单——只需通过类型本身的键来索引类型:*

```
*type AllGuests<M> = IPsToGuests<M>[keyof IPsToGuests<M>];*
```

# *结论*

*TypeScript 拥有令人印象深刻的处理复杂类型的能力。然而，如果没有很好地掌握基础知识，很容易迷失在关键字、类型操作符和泛型中。深入思考甚至最简单的类型有助于逐渐建立对更复杂类型的直觉，这有助于您构建更健壮和可伸缩的 TypeScript 应用程序。*

**更多内容看* [***说白了. io***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) ***。*** *在我们的**[***社区不和谐***](https://discord.gg/GtDtUAvyhW) ***中获取独家写作机会和建议。*****