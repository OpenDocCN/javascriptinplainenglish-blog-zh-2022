# 通过使用转换器提高 JavaScript 中的映射性能

> 原文：<https://javascript.plainenglish.io/improve-mapping-performance-in-javascript-by-using-transducers-618696a85cb5?source=collection_archive---------1----------------------->

![](img/bb836fd848163dcef975620b804cd02e.png)

Photo by [Markus Winkler](https://unsplash.com/@markuswinkler?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

传感器是一种将一组数据转换成另一组数据的功能。在函数式编程的上下文中，转换器是一个高阶函数，它接受一个缩减函数，并返回一个在某种程度上更有效的新缩减函数。这对于加速处理大量数据的函数非常有用。

用传感器加速减少功能的一种方法是利用懒惰。这意味着转换器只在需要时对集合的每个元素执行必要的转换，而不是预先对整个集合执行所有转换。这对于减少具有短路行为的函数特别有用，例如`takeWhile`或`find`。

另一种用传感器加速还原功能的方法是使用合成。这意味着转换器由较小的转换器组合而成，每个转换器对集合执行特定的转换。这允许换能器在集合上的单次通过中执行多次变换，降低了缩减函数的总时间复杂度。

下面是一个传感器的例子，它利用懒惰和合成来加速减少功能:

```
const filterMap = pred => mapFn => (acc, x) =>
  pred(x) ? mapFn(acc, x) : acc;

const filterMapReducer = filterMap(predicate)(mappingFunction);

const transducedReducer = transduce(
  filterMapReducer,
  reducer,
  initialValue,
  collection
);
```

在这个例子中，`filterMap`转换器将一个谓词函数和一个映射函数作为参数。它返回一个新的 reducing 函数，该函数只将映射函数应用于满足谓词的集合元素。这允许换能器跳过不需要变换的元素，从而降低缩减函数的时间复杂度。

`filterMap`传感器可以与其他传感器组合，在一次扫描中对集合执行多次转换。例如，您可以使用`map`和`filter`传感器以如下方式转换集合:

```
const doubleEvenNumbers = map(x => x * 2);
const keepPositiveNumbers = filter(x => x > 0);
const transducer = compose(doubleEvenNumbers, keepPositiveNumbers);
const transducedReducer = transduce(transducer, reducer, initialValue, collection);
```

在这个例子中，`transducer`是由`doubleEvenNumbers`和`keepPositiveNumbers`传感器组成的。它会将集合中的每个偶数加倍，只保留正数，跳过所有其他元素。这允许换能器在集合上的单次通过中执行两种变换，从而降低缩减函数的时间复杂度。

总的来说，传感器是一个强大的工具，可以加速处理大量数据的功能。它们允许你利用懒惰和合成来减少减少函数的时间复杂度，使它们更高效和可伸缩。

希望这有所帮助！

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

报名参加我们的 [**免费周报**](http://newsletter.plainenglish.io/) 。关注我们 [**推特**](https://twitter.com/inPlainEngHQ) ，[**LinkedIn**](https://www.linkedin.com/company/inplainenglish/)**，**[**YouTube**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)**，** [**不和谐**](https://discord.gg/GtDtUAvyhW) **。**

## 想用内容来扩展你的科技创业吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。

我们提供免费的专家建议和定制解决方案，帮助您建立对您的技术产品或服务的认知和采用。