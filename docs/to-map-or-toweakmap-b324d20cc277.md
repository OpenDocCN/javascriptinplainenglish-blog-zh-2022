# 在 JavaScript 中什么时候应该使用 Map & WeakMap

> 原文：<https://javascript.plainenglish.io/to-map-or-toweakmap-b324d20cc277?source=collection_archive---------5----------------------->

## 了解什么是 WeakMap，它的用例，它与 Map 有何不同，以及何时应该在 JavaScript 中使用 Map & WeakMap。

![](img/25a71f5523ce7fd4f43a537d295e0f80.png)

JavaScript 提供了许多内置对象，帮助 JavaScript 开发人员的生活变得简单而轻松。这些众所周知的物体包括但不限于:

*   排列
*   日期
*   JSON
*   地图
*   承诺

然而，JavaScript 也有一些不常见的内置对象，如果使用得当，可以显著提高 JavaScript 应用程序的性能。

这些物品中的一个是 WeakMap。

# 什么是 WeakMap？

根据 MDN，WeakMap 可以定义为“一组键/值对，它们的键**必须是具有任意 [JavaScript 类型](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#javascript_types)值的对象**、**和**，并且不会创建对其键的强引用”

你会注意到我加粗并强调了“必须是对象”,因为这是理解 WeakMap 并将其与常规的 [Map](https://medium.com/analytics-vidhya/deep-dive-into-javascript-map-object-24c012e0b3fe) 对象区分开来的关键点之一。

简单来说，WeakMap 允许以一种独特的方式将数据与对象关联起来，一旦对象不再被引用，就允许对数据进行垃圾收集。

## WeakMap 和地图有什么不同？

WeakMap 派生自一个 Map 对象，虽然语法上非常相似，但在方式上也有很大不同。

## 差异:

**用 JavaScript 映射对象**:

1.  您可以将映射的键设置为任何 JavaScript 类型，如对象和原语。
2.  它创建了对其键的强引用
3.  允许枚举，这意味着可以使用 forEach()、keys()、values()等方法来获取映射的键和值的列表。

**至于 WeakMap:**

1.  弱映射**的键必须**是对象类型。任何其他值都将引发错误。
2.  它不会创建对其键的强引用。
3.  它不允许枚举，这意味着您不能使用 keys()、values()或 entries()等方法来获取键或值的列表
4.  允许对任何值进行垃圾收集，如果它们的键对象不是从 WeakMap 之外的任何地方引用的。

## 相似之处:

WeakMap 和地图支持方法，例如:

*   获取()
*   集合()
*   有()
*   删除()

## 我们如何实现 WeakMap？

现在我们已经有了理论，让我们看看实现一个 WeakMap 对象有多容易。

可以通过调用新方法来构造 WeakMap。没有它，将会抛出一个错误。

```
const weakMap = new WeakMap();
```

为 WeakMap 设置键和值:

```
const user1 = {name: 'Kwadjo'} //Requires the key to be of an objectweakMap.set(user1, '22');
```

从 WeakMap 返回元素就像调用 get()方法一样简单。

```
console.log(weakMap.get(user1)) // Returns "22"
```

## 垃圾收集:

如前所述，Map 和 WeakMap 的主要区别在于[垃圾收集器](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Memory_Management)。

让我们快速回顾一下垃圾收集。

JavaScript 可以在对象创建时自动为它们分配内存，并在它们不再被使用时释放它们。后一部分就是所谓的垃圾收集。

给定下面的例子，其中我们创建一个对象:

```
let user2 = { name: "Afia" };
```

JavaScript 将为它分配内存，这将允许对象被访问。常量 user2 将是对它的引用。

如果我们现在要覆盖用户 2 的引用:

```
user2 = null;
```

![](img/79b25b4d4671b967f27cc75420e0226c.png)

这将把对象标记为垃圾回收并从内存中移除。

## 嗯，那么这如何适用于地图和 WeakMap？

假设我们创建一个对象，并将其设置为地图对象的键:

```
let user3 = { name: "Obenewaa" };let map = new Map();map.set(user3, 'hello');
```

如果我们使用 console.log map，我们将得到:

```
console.log(map);//Output: {{   "name": "Obenewaa" } => "hello"}
```

回想一下我前面提到的 Map 创建了对其键的强引用。让我们通过将 user3 设置为 null 并在控制台记录输出来测试这一点:

```
user3 = null;console.log(map);//Output: {{   "name": "Obenewaa" } => "hello"}
```

您会注意到，虽然我们覆盖了 user3 的引用，但是 Map 对象仍然保留了对该对象的强引用。因此，尽管调用 Map 对象的 get()方法将返回 undefined，但其他方法(如 h as()或 forEach()仍将能够返回该对象。

> 这是因为随着 Map 对象的继续存在，该对象也将继续存在，并防止它被垃圾收集。

让我们在 WeakMap 上试试这个:

```
let user3 = { name: "Obenewaa" };let weakMap = new WeakMap();weakMap.set(user3, 'hello');
```

因为 WeakMap 是不可枚举的，所以我们必须使用 get()方法来输出值:

```
console.log(weakMap.get(user3)) // 'hello'
```

如果我们现在将 user3 重写为 null，并尝试输出该值，我们将得到未定义的值:

```
user3 = null;
console.log(weakMap.get(user3)); //returns undefined
```

因为 WeakMap 不创建对其键的强引用，所以它不会阻止对象被垃圾收集。

## **但是等等！为什么 WeakMap 不支持任何可迭代的方法？**

这又与垃圾收集有关。如果一个对象丢失了对它的所有其他引用，那么一旦垃圾收集器运行，它将被标记为垃圾收集。关于垃圾收集器要知道的是，它不在指定的时间运行，这意味着对未使用对象的垃圾收集可以立即发生，也可以在以后发生。

![](img/58d5919ce910f099075dab66c8e297f4.png)

这意味着，WeakMap 不知道它的计数或大小，因为垃圾收集可能已经清理了它的键或部分清理了它的一些键。

# 我什么时候应该使用地图或 WeakMap

确定何时使用地图或 WeakMap 的简单方法是:

*   如果你想要一个键列表或者需要枚举，使用一个**图。**
*   如果你需要对象的键在不再被引用后被处理掉，而不是保存在内存中——使用一个 **WeakMap。**

## WeakMap 的使用案例:

WeakMap 的用例不会像常规地图那样多，但 WeakMap 的主要用例是防止内存泄漏，或者您的地图需要对象作为键，一旦对象完成其使用，就应该从内存中释放对象。

您是否使用过 WeakMap 对象或者对它不熟悉？请在下面留下您对 WeakMap 对象的想法和使用案例的评论。

如果你喜欢这篇文章，看看我下面的其他文章:

*   [**深度潜入 JavaScript 地图对象**](https://medium.com/analytics-vidhya/deep-dive-into-javascript-map-object-24c012e0b3fe)
*   [**动态添加和移除角形**](https://medium.com/javascript-in-plain-english/dynamically-add-and-remove-canactivate-route-guards-in-angular-e7820ab4e061) 中的可激活守卫
*   [**AOP-Routing Library for Angular**](https://medium.com/analytics-vidhya/the-aop-routing-library-for-angular-9ada05f1741d)
*   [**什么是类型脚本元组**](https://medium.com/@ericsarpong/what-is-a-typescript-tuple-814a016f61fd)
*   [**简单地说异步编程(理论)**](https://ericsarpong.medium.com/asynchronous-programming-in-a-nutshell-theory-d5fd07cf3b22)
*   [**角路由:命令式 vs PopState**](https://medium.com/p/7d254b495c54/edit)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***