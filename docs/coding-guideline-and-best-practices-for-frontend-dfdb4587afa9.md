# 15 前端编码指南和最佳实践

> 原文：<https://javascript.plainenglish.io/coding-guideline-and-best-practices-for-frontend-dfdb4587afa9?source=collection_archive---------1----------------------->

## 遵循这些编码指南并采用这些最佳实践来确保代码质量和无错误代码。

![](img/8a56eece5463364cd24a22ae77193f1a.png)

Photo by [Christopher Gower](https://unsplash.com/@cgower?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

为了确保代码质量和无 bug 代码，我们应该遵循一些指南和最佳实践。我正在分享我和我的团队遵循的指导方针。

## **1。你应该在你的项目**中设置 ESLint 和 Husky

ESLint 可以快速发现代码中的问题，并给出解决这些问题的建议。这也使得代码审查者的任务变得容易。

Husky 改进您的代码提交。如果我们正确配置了 Husky，它就不会让开发人员在代码中出现错误或测试用例失败时提交他们的代码。

## **2。遵循坚实的原则**

扎实的原则很重要。写代码时，你应该牢记坚实的原则。例如，一个功能不应该做一个以上的任务。(单一责任)。

**固体原理代表:**

1.  **S —单一责任原则**
2.  **O —开闭原理**
3.  **L —利斯科夫替代原理**
4.  **I —界面偏析原理**
5.  **D —依存倒置原则**

## **3。代码中的文件**

您应该为您的代码编写技术文档，以便任何新开发人员都能轻松理解。

可以用 JSDoc 做文档。这个文档也可以导出，对理解代码很有帮助。在 JSDoc 中，你应该描述你已经创建的函数或组件。应该提到属性/参数的确切数据类型。您不应该给出数据类型的超集(例如，所有类型的对象)。

你可以从[这里](https://jsdoc.app/about-getting-started.html)阅读更多关于 JSDoc 的内容

## **4。应避免过度使用业绩挂钩**

深入了解 React 挂钩，并明智地使用它们。不应到处使用 useMemo、useCallback、React.memo。

## **5。不要重复自己(干)**

您应该创建可重用的组件和函数，以避免重复编写相同的代码。

《出埃及记》util 函数、钩子、hoc 等。

## **6。注意可访问性**

您的应用程序应该是每个人都可以访问的，例如残疾人、移动设备、慢速网络等。它应该很容易用键盘操作。

你可以在这里阅读更多关于可访问性的信息。

## 7。编写单元和集成测试用例

我们应该编写测试用例来检查业务逻辑。如果我们正在进行增强，并且任何受到影响的业务逻辑只能在开发阶段被捕获，这将会有所帮助。

## **8。将开发依赖与生产依赖分离**

## **9。使用命名导入而不是析构。**

**不正确**

```
import { isArray} from “lodash”;
```

**正确**

```
import isArray from “lodash/isArray”;
```

## **10。使用适当的消息频繁提交**

我们应该提交我们的代码，如果我们完成任何小功能，并应在一天结束时编码。

## **11。使用更严格的变量声明，函数**

避免使用 var。开始使用 let 和 const。如果事情不会改变，我们应该只使用常量。

## **12。避免在循环中使用变量**

我们应该避免在循环中声明变量。它可能会不必要地消耗内存。

## **13。清理存储器**

尽管 javascript 负责清理内存，但有时我们也需要清理内存，比如 settimeout 或 setinterval。

在 React 中，你可以在 [componentWillUnmount](https://reactjs.org/docs/react-component.html#componentwillunmount) 中处理这些事情，或者使用 effect 钩子返回一个你可以取消订阅、cleartimeout 或 clearInterval 的函数。

## **14。性能优化**

有几种方法可以优化性能。

1.  缩小并压缩你的包
2.  CDN 和浏览器级缓存
3.  本地存储和会话存储的使用
4.  PWA 应用
5.  分页或无限滚动
6.  去抖/节流的使用[https://santoshyadav 979439 . medium . com/debounting-in-Java-script-b 8d 63 c 34 feec](https://santoshyadav979439.medium.com/debouncing-in-java-script-b8d63c34feec)
7.  中止控制器的使用
8.  如果您正在 React 中开发应用程序，React 性能挂钩
9.  延迟加载等

## 15。安全性

我们还应该注意安全部分。

我们可以做的几件事是:

1.  受限文件上传
2.  在前端和后端验证表单输入和净化应用程序。这方面可用的库很少。这样我们可以减轻 XSS 的攻击。我们还应该启用 XSS 保护模式。
3.  验证码的使用
4.  使用强大的内容安全策略。(CSP)
5.  禁用 iframe 嵌入
6.  保持错误的一般性
7.  使用有限的浏览器功能和 API
8.  避免使用第三方库。库中可能有恶意代码。

这个题目到此为止。感谢您的阅读。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***