# 关于 React 中的记忆，你应该知道的 3 件事

> 原文：<https://javascript.plainenglish.io/3-things-you-should-know-about-memoization-in-react-b2f09570bb53?source=collection_archive---------19----------------------->

## 在 React 项目中使用记忆方法之前，每个开发人员都应该知道的三件事。

![](img/cebedcb801ea27f2cb12ba3fe30bdf03.png)

记忆是一种缓存计算量很大的函数的结果的技术。在 React 中，我们可以使用这种技术来避免不必要的重新渲染和昂贵的重新计算。React 为此提供了三种方法:

*   **memo** :用于记忆组件的高阶组件。
*   **useMemo** :用于记忆一个计算代价很高的值的钩子
*   **useCallback** :类似于 useMemo，用于记忆一个回调函数。

尽管内存化对于提高性能很有帮助，但是如果使用不当，它可能会产生相反的效果。让我们看看在 React 项目中使用这些方法之前应该注意的三件事。

# 1.内存化意味着性能优化

除非在应用程序中遇到性能问题，否则使用任何记忆方法都不是一个好主意。你的代码应该在没有记忆的情况下工作(不管它有多慢)。根据经验，您应该在实现组件后考虑优化。

如果您注意到性能问题，React DevTools 可以帮助您找到性能瓶颈。但是也要记住，记忆化并不能解决所有的性能问题。因此，最好总是检查是否从中获得了任何改进。

此外，要警惕过早的优化，这样你就不会在没有必要的情况下浪费时间进行优化。JavaScript 中的大多数操作都经过了优化，总体而言，React 框架的性能非常好。因此，在大多数情况下，可能不需要进一步的优化。

# 2.内存化有性能开销

性能优化通常伴随着一些权衡。记忆化尤其如此。通过缓存以前的结果，我们使用更多的内存来提高速度。所以，你应该经常考虑记忆的成本是否值得。这取决于用例，但值得注意的是，如果性能改善不明显，使用它会有额外的开销。

# 3.反应并不总是保证记忆

在 React 文档上，如果您看到[使用备忘录](https://reactjs.org/docs/hooks-reference.html#usememo)上的部分，内容如下:

您可以依赖 useMemo 作为性能优化，而不是作为语义保证。

如果你也看看文档中的 [React.memo](https://reactjs.org/docs/react-api.html#reactmemo) ，你会发现:

这种方法仅作为性能优化而存在。不要依赖它来“阻止”渲染，因为这会导致错误。

React 将尽可能长时间地缓存结果，但在某些情况下，它也可能选择使缓存无效。因此，不能保证记忆的值没有被丢弃。这意味着你不能依赖 React 总是为你记忆价值观。为了避免在应用程序中引入错误，请始终使用内存化方法来优化性能，仅此而已。

# 结论

我希望你现在已经掌握了在负责任的反应中使用记忆所需要的所有信息。请分享您的意见和建议，感谢您的阅读。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*