# 如何在 JavaScript 中检查等式

> 原文：<https://javascript.plainenglish.io/how-to-check-equality-in-javascript-d8742a990fd?source=collection_archive---------8----------------------->

## 创建一个函数来检查对象是否相等

![](img/049d1e91ac9ba2a7a1c0faa5479a3c4b.png)

Photo by [Pedro Figueras](https://www.pexels.com/@pedro-figueras-202443/) on [pexels](https://www.pexels.com/photo/two-pigeon-perched-on-white-track-light-681447/)

最近我在做一个项目，我必须检查两个对象是否有相同的数据点。这是我以前做过的一项任务，所以我认为我过去的一些解决方案可能会奏效。事实证明，我之前实施的解决方案不起作用。它不处理嵌入对象、嵌入数组或未定义/空数据类型等情况。考虑到这一点，我决定重新创建一个解决方案来处理所有这些情况(如果您发现一个测试用例使这个解决方案失败，请确保在评论中删除它)。在这篇博客中，我将讨论我的思考过程，以及我是如何创造出解决这个问题的方案的。

另一件需要注意的重要事情是，已经存在 npm 解决方案来为您处理这个问题。例如，npm Lodash 有一个 [isEqual](https://lodash.com/docs/4.17.15#isEqual) 函数来检查对象之间的相等性。然而，当我需要的只是一个单一的函数时，我不想安装这么大的软件包。

在我们开始之前，你也可以看看这篇由 Sankalp Lakhina 撰写的[博客，以了解为什么在 JavaScript 中检查`obj1 === obj2`不起作用。](https://medium.com/@sankalp.lakhina91/understanding-object-equality-in-javascript-ec3e7a2b5b1d)

## 最终答案

为了节省那些只需要答案的读者的时间，我把我的解决方案放在顶部。博客的其余部分将涵盖我的工作流程/测试案例。

## 设置

为了快速准确地测试我正在创建的`isEqual`函数，我将编写许多测试用例。我将使用`Jest`运行这些测试用例。如果你不确定如何编写测试用例，你可以看看我的博客。在接下来的几节中，您将能够看到我创建的测试用例。

## 第一步:简单的物体

我从处理“简单对象”开始。我将“简单对象”定义为不包含嵌入对象的对象。“简单对象”仅由 JavaScript [原始类型](https://developer.mozilla.org/en-US/docs/Glossary/Primitive)组成。根据 MDN Web 文档的定义，JavaScript 只有 7 种原始数据类型:[字符串](https://developer.mozilla.org/en-US/docs/Glossary/String)，[数字](https://developer.mozilla.org/en-US/docs/Glossary/Number)， [bigint](https://developer.mozilla.org/en-US/docs/Glossary/BigInt) ，[布尔](https://developer.mozilla.org/en-US/docs/Glossary/Boolean)，[未定义](https://developer.mozilla.org/en-US/docs/Glossary/undefined)，[符号](https://developer.mozilla.org/en-US/docs/Glossary/Symbol)，以及[空值](https://developer.mozilla.org/en-US/docs/Glossary/Null)。

注意:我排除了符号的测试用例。符号是一种唯一的数据类型，其中创建的每个符号都应该是唯一的，除非它们是用`.for()`方法创建的。你可以在这里阅读更多关于符号[的内容。](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol)

我从创建以下测试用例开始。

下面你可以看到我的解决方案。

有了这个解决方案，除了两个之外，所有的测试用例都通过了。第一个问题是关于`NaN`值。`NaN === NaN`评估为`false`，然而，我期望这个评估为`true`。为了解决这个问题，我将首先检查传递的值是否属于类型`number`，并使用 JavaScript 的内置函数`Number.isNaN()`检查它们是否为`NaN`。如果是这样，我就返回`true`。

第二个问题是关于`null`原始类型。`Null`属于 JavaScript 中的`object`类型，必须被隐式检查。简单地在函数顶部添加一个隐式的`null`值检查应该可以解决这些问题。

下面你可以看到`isEqual`函数是如何被修改的。

然后我写了应该评估为`false`的测试用例。

这些测试案例发现了新的错误。首先，让我们解决一个对象的值设置为`undefined`而另一个对象缺少键的情况。为了解决这个问题，我决定添加一个`if`条件和另一个循环。我将首先检查两个对象是否有相同数量的键。如果对象有不同数量的键，我将立即返回`false`。接下来，我将遍历 object1 的键，并确保它们出现在 object2 中。如果钥匙不在，我会马上归还。这个增加应该可以处理对象看起来像这样的测试用例。

在本节中，我不会在每个键上递归调用`isEqual`。原因在于，只要对象具有相同的键值对，它们就应该被认为是相等的。它们的键的顺序并不重要。

新的和更新的代码和测试用例应该是这样的。

现在我们可以继续解决更复杂的物体。

## 第二步:复杂的物体

幸运的是，我们的解决方案应该足够健壮，能够处理嵌入式对象。我创建了下面的测试用例只是为了确保。

在运行这些测试用例之后，我们可以看到嵌入的对象正在按预期工作。

## 第三步:列表

测试列表之间的相等性应该很容易。首先，我将检查传递的值是否是列表。接下来，我将检查它们是否长度相同。如果它们长度相同，那么我将遍历列表，递归地调用每个元素上的`isEqual`。如果元素不相等，我将返回`false`。最后，如果列表长度不等，那么我将返回`false`。下面你可以看到我做的测试用例以及代码是如何修改的。

## 第四步:集合

最后，我想在 set 上测试我的解决方案。下面你可以看到我做的测试案例。

正如所料，当前的解决方案不起作用，但是，这有一个简单的解决办法。在运行数组逻辑之前，我将检查传递的值是否是一个`instanceof Set`。如果它们都是集合，我将把它们转换成数组，对它们进行排序，并对排序后的数组运行`isEqual`逻辑。我必须对它们进行排序，因为集合和对象一样，只要包含相同的值，就应该被评估为`true`。顺序应该无关紧要。如果不是两套，我就返回`false`。更新后的代码应该如下所示。

通过这个简单的加法，我们完成了`isEqual`函数。希望这对你有帮助。

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*