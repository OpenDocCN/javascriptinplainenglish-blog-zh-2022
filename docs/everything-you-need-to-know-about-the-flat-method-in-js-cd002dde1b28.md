# 关于 JS 中的 flat()方法，您需要知道的一切

> 原文：<https://javascript.plainenglish.io/everything-you-need-to-know-about-the-flat-method-in-js-cd002dde1b28?source=collection_archive---------3----------------------->

你听说过 JavaScript 中的 flat()方法吗？JavaScript 中的 flat()方法是一个强大的工具，用于操作数组并将它们展平为一个单一的一维列表。当处理具有复杂结构的嵌套数组或数据集时，这尤其有用。使用 flat()方法，您可以轻松地将数组展平到任何所需的深度，从而简化数据的处理和操作。无论您是初学者还是有经验的 JavaScript 开发人员，flat()方法都是使用数组的工具箱中必不可少的一部分。在本文中，我们将深入探讨 flat()方法如何工作的细节，如何使用它来简化代码，以及使用 flat()的潜在陷阱和如何避开它。

这只是 generell 中许多关于 JavaScript 或软件开发的文章之一。通过关注和订阅，一定不要错过任何精彩的文章。

![](img/9ee268ac1b974671b854a1a93e8101b2.png)

Photo by [Food PhotoGraphy Mumbai](https://unsplash.com/@foodphotographymumbai?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 JavaScript 中，flat()方法用于将数组展平到指定深度。它创建一个新数组，所有子数组元素递归连接到该数组中，直到指定的深度。

以下是如何使用 flat()方法的示例:

```
const array = [1, 2, [3, 4, [5, 6]]];
const flatArray = array.flat();
console.log(flatArray); // [1, 2, 3, 4, [5, 6]]
```

在本例中，flat()方法将数组展平到深度 1，因此子数组[3，4，[5，6]]没有展平。

您可以指定大于 1 的深度，以将阵列展平到更大的深度。例如:

```
const array = [1, 2, [3, 4, [5, 6]]];
const flatArray = array.flat(2);
console.log(flatArray); // [1, 2, 3, 4, 5, 6]
```

在这个示例中，flat()方法将数组展平到深度 2，因此与前面的示例相反，子数组[5，6]也被展平。

## 优点和缺点

以下是使用 flat()方法的一些优点:

*   它可以简化您的代码:如果您有一个包含嵌套子数组的数组，并且您需要访问或修改子数组的元素，您将不得不使用嵌套循环或递归函数来实现这一点。使用 flat()方法，您可以展平数组并直接访问或修改元素，这可以使您的代码更简单、更易读。
*   它可以提高代码的性能:如果您有一个包含许多嵌套子数组的大型数组，在对数组执行操作之前使用 flat()方法展平数组可以提高代码的性能，因为它减少了所需的迭代次数。
*   它可以使处理数据变得更容易:如果数据存储在嵌套的数组结构中，使用 flat()方法可以使处理数据变得更容易，因为您可以直接访问元素，而不必在嵌套结构中导航。

在 JavaScript 中使用 flat()方法也有一些潜在的缺点:

*   旧版本的浏览器可能不支持该方法:并非所有浏览器都支持 flat()方法，因此如果您需要支持旧版本的浏览器，您可能需要使用 polyfill 或其他方法来拼合数组。
*   对于大型数组，它可能不会像预期的那样工作:当用于非常大的数组时，flat()方法可能会很慢，因为它必须迭代数组及其子数组的所有元素。这可能会导致性能问题，尤其是当您需要将数组展平到非常深的级别时。
*   这可能不是展平数组的最有效方法:根据代码的特定要求，可能有其他方法或技术可以更有效地展平数组。例如，在某些情况下，使用循环或递归函数手动展平数组可能会更快。
*   它可能并不适合所有类型的数据:flat()方法是为处理数组而设计的，因此它可能不是展平其他类型数据结构的最佳选择。
*   这是不可能恢复的:一旦对数组应用了扁平化操作，就不能取消数组的扁平化。一旦执行了 flat 函数，原始结构就永远丢失了。有很多方法可以解决这个问题，下面我会告诉你。

虽然 flat()方法在某些情况下可能是一个有用的工具，但是考虑它的局限性以及它是否是满足您的特定需求的最佳选择是很重要的。

我们想要特别解决上面提到的关于 JavaScript 中 flat()方法的恢复和替代的限制。

## 恢复 flat()操作

目前无法在 JavaScript 中直接恢复 flat()操作。一旦数组被展平，数组的原始结构将永远丢失。

但是，如果需要恢复数组的展平，可以在展平之前将数组的原始结构存储在一个单独的变量中，然后使用该信息来重建原始数组。

下面是一个如何做到这一点的示例:

```
// Flatten the array
const array = [1, 2, [3, 4, [5, 6]]];
const structure = array.map(element => Array.isArray(element) ? element : null);
const flatArray = array.flat();
// Revert the flattening
function revertFlattening(flatArray, structure) {
 let index = 0;
 return structure.map(element => element ? element.map(() => flatArray[index++]) : flatArray[index++]);
}
const originalArray = revertFlattening(flatArray, structure);
console.log(originalArray); // [1, 2, [3, 4, [5, 6]]]
```

在本例中，我们在展平数组之前，将数组的原始结构存储在结构变量中。然后，我们使用 revertFlattening()函数通过迭代 flatArray 和结构变量来重建原始数组，并根据 structure 中存储的结构将 flatArray 中的元素插入到原始数组中的正确位置。

这种方法需要存储有关数组原始结构的附加信息，并且它可能不适合所有情况。它也可能比 flat()方法本身要慢，所以如果您需要在大型数组上频繁执行拼合和恢复操作，它可能不是最佳选择。

## 平面的替代物()

如果您需要在 JavaScript 中展平一个数组，而 flat()方法不可用或不适合您的需要，您可以考虑一些替代方法:

*   使用循环:您可以使用循环来迭代数组及其子数组的元素，并将元素添加到新数组中。以下是如何使用循环展平数组的示例:

```
function flattenArray(array) {
  let flattened = [];
  for (let element of array) {
    if (Array.isArray(element)) {
      flattened = flattened.concat(flattenArray(element));
    } else {
      flattened.push(element);
    }
  }
  return flattened;
}
const array = [1, 2, [3, 4, [5, 6]]];
const flatArray = flattenArray(array);
console.log(flatArray); // [1, 2, 3, 4, 5, 6]
```

*   使用扩展运算符:您可以使用扩展运算符(…)将数组及其子数组的元素扩展到一个新数组中，从而展平数组。以下是如何使用 spread 运算符展平数组的示例:

```
function flattenArray(array) {
 return array.reduce((acc, val) => acc.concat(Array.isArray(val) ? flattenArray(val) : val), []);
}
const array = [1, 2, [3, 4, [5, 6]]];
const flatArray = flattenArray(array);
console.log(flatArray); // [1, 2, 3, 4, 5, 6]
```

*   使用 concat()方法:您可以使用 concat()方法，通过将数组及其子数组的元素连接成一个新数组来展平数组。以下是如何使用 concat()方法展平数组的示例:

```
function flattenArray(array) {
  let flattened = [];
  for (let element of array) {
    if (Array.isArray(element)) {
      flattened = flattened.concat(flattenArray(element));
    } else {
      flattened = flattened.concat(element);
    }
  }
  return flattened;
}
const array = [1, 2, [3, 4, [5, 6]]];
const flatArray = flattenArray(array);
console.log(flatArray); // [1, 2, 3, 4, 5, 6]
```

这些只是在 JavaScript 中如何展平数组的几个例子。根据您的具体需求，您可能还可以使用其他方法或技术。

## 例子

JavaScript 中的 flat()方法在许多需要处理包含嵌套子数组的数组的情况下非常有用。以下是 flat()方法的一些用例示例:

*   在处理数组之前将其展平:如果您有一个包含嵌套子数组的数组，并且您需要对子数组的元素执行操作，那么您可以使用 flat()方法在处理数组之前将其展平。这可以简化您的代码，使处理数据更加容易。
*   在存储数组之前将其展平:如果数据存储在嵌套数组结构中，并且希望将其存储在平面结构中，可以使用 flat()方法在存储数组之前将其展平。这使得以后检索和处理数据变得更加容易。
*   在显示数组之前将其展平:如果数据存储在嵌套的数组结构中，并且希望以平面结构显示它，可以使用 flat()方法在显示数组之前将其展平。这使得向用户呈现数据变得更加容易。
*   排序前展平数组:如果您有一个包含嵌套子数组的数组，并且您想要排序子数组的元素，您可以使用 flat()方法在排序前展平数组。这可以使排序更容易，因为您可以直接比较元素。

总而言之，flat()方法在各种需要使用 JavaScript 中嵌套数组的情况下非常有用。有优点也有缺点，您必须针对您的具体情况评估使用 flat()方法是否有意义。决定的标准包括性能、数组大小，以及 flat()方法在相关环境中的可用性。但是尽管有这些限制，我们也讨论了如何规避它们。

![](img/5c7fdb823e2c7f4190f716ff6bed224c.png)

所以，就这样了。我们希望你了解了公寓的功能和功能，以及如何解决这个问题。你不会经常遇到这种情况。因此，我们建议您稍后再看这篇文章。如果你喜欢，可以和你的同事分享。还可以考虑关注或订阅我们，获取更多关于 JavaScript 或软件开发的精彩内容。

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。跟随我们登上* [***推特***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*和****T40**T44**

## **想扩大你的软件启动规模吗？查看[电路](https://circuit.ooo/?utm=publication-post-cta)。**