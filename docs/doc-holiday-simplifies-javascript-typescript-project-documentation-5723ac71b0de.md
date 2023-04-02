# Doc-Holiday 简化了 JavaScript/TypeScript 项目文档

> 原文：<https://javascript.plainenglish.io/doc-holiday-simplifies-javascript-typescript-project-documentation-5723ac71b0de?source=collection_archive---------25----------------------->

## Doc-Holiday 如何简化 JavaScript/TypeScript 项目文档。

![](img/f058e76d1391f62370aec5b5ee7f001e.png)

Illustration licensed from istockphoto.com

如果你有一些使用 JavaScript 的经验，你可能用过 JSDoc。您可能对从编写良好的源代码中获得“自动”API 文档来呈现合理的结果感到沮丧。

与其他生成的文档的混乱结果相比，您最终得到的文档可能看起来是合理的。然而，您的源代码注释块现在充斥着许多“@”符号。

为什么？

JSDoc 是在很久以前 JavaScript 还是新事物的时候创建的。像类和枚举或接口、混合或类型定义这样的结构在语言中并不正式存在。然而，JavaScript 专家找到了从 JavaScript 当时使用的过程结构中创建这些结构的方法。今天，您可以使用' class '关键字来定义一个类，但在' class '关键字存在之前,' class '构造概念是通过创建函数和向函数原型添加成员来完成的。

当然，这意味着文档工具需要被告知一个函数被当作一个@类，并且相关的成员声明是该类的一个@ member。

JSDoc 现在可以识别代码中用 class 关键字声明的类，但是其他几个概念，比如枚举和类型定义，根本没有纯 JavaScript 语言支持，必须在源代码注释块中使用经常令人困惑的 JSDoc 标记来编写。

我使用 TypeScript 已经有一段时间了，关于 TypeScript 最棒的事情之一就是它的类型。如果我编写一个函数并声明参数的类型，例如:

```
function Foo(bar:string, baz:number) {}
```

为什么我还必须在函数注释中包含@param 声明来记录这些内容呢？

JSDoc 不能很好地与 TypeScript 一起工作。它不会直接处理. ts 文件。但是，因为注释是从 ts 源传递过来的，所以您可以针对。TypeScript 编译器创建的 js 文件。这是可行的，但也有缺点。您仍然需要在函数块中包含@param 和@return 标记，并且类的结构并不理想。这需要冗余来捕获任何类型的定义或枚举的文档。

## 介绍 Doc-Holiday

Doc-Holiday 是一个免费的开源项目，可以从 NPM 下载，旨在减轻这些挫折。

可以在 [@tremho/doc-holiday](https://www.npmjs.com/package/@tremho/doc-holiday) 下的 [npm](https://www.npmjs.com) 找到

它的工作方式不同于其他 JSDoc 兼容的文档引擎——它不是 HTML/Markdown 呈现引擎。相反，它是一个中介，从 TypeScript 或 JavaScript 文件中生成合理的 JSDoc 就绪源代码存根，然后调用您选择的呈现引擎将其转换为 HTML 或 Markdown 以供发布。

JSDoc 社区为您的输出方式提供了全面的支持，您可以使用各种专业外观的模板和主题。此外，您可以避免在重复您已经定义的代码时必须添加显式 JSDoc 标记的缺陷。

Doc-Holiday 允许您为 jsdoc 渲染引擎使用 jsdoc、jsdoc2md 或 documentation JS。

documentation JS 的出发点与 Doc-Holiday 基本相同。它简化了 JSDoc 的使用，从源代码中推断出更多的内容，并将大量 JSDoc 标签减少和规范化到一个合理的可管理的数量。它还为 HTML 和 Markdown 提供了清晰一致的文档输出。

然而，*文档 JS* 不支持类型脚本，因此也不容易支持类属性、接口、类型定义或枚举之类的东西。

尽管 Doc-Holiday 也能很好地处理传统的 JavaScript，但它一开始就被设计成支持类型脚本的。它可以识别许多模式，这些模式可以建立一个代码实体及其可记录的属性，并在文档处理期间将这些转换成 JSDoc 兼容的块，因此您不必这样做。您的源代码可以保持相对干净和可读性。

[Doc-Holiday](https://tremho.github.io/docholiday/) 还有一些其他有趣的功能:

*   记录内部类的能力
*   记录自定义类型定义和回调的能力
*   能够识别和记录混音和界面
*   [引入约束](https://tremho.github.io/docholiday/constraints) —关于所有类型的值的值范围的规范，记录了可接受的值是什么样子，并且可以在运行时强制执行。
*   [PlantUML 图表](https://plantuml.com) —支持任何 PlantUML 图表语言指令，以便在您的代码注释中制作出美观且信息丰富的图表。
*   除了源代码生成的 API 文档之外，还支持相关文档的发布。
*   Doc-Holiday 既是一个命令行工具，也是一个 Node.js 模块，它公开了一个可在定制文档管道中使用的编程 API。

总而言之，Doc-Holiday 是一个受欢迎的突破，它打破了之前的激烈争论。

*披露:Steven Ohmert 是@tremho/doc-holiday* 的作者

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于**[***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。**