# 提高打字稿类型安全性的 3 种方法

> 原文：<https://javascript.plainenglish.io/runtime-type-checking-in-typescript-c725d83e12c1?source=collection_archive---------5----------------------->

## 修正这个打字稿缺陷，有利弊

TypeScript 已经成为 JavaScript 的首选。它具有出色的 IDE 支持，简化了大型代码库的工作，改善了团队协作，并防止了错误。然而，与传统的类型语言相比，它也有明显的差距。

![](img/fbef0b02ff664d75acee0ae926b25928.png)

Photo by [Brian McGowan](https://unsplash.com/@sushioutlaw?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

TypeScript 不同于其他传统的类型化语言。在 C#和 Java 中，类型是一等公民，这些语言内置了类型，而 TypeScript 是常规 JavaScript 之上的语法层。面向 OOP 开发人员的 TypeScript 页面是很好的读物；以下摘自[那页](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-oop.html):

*在 C#或 Java 中，任何给定的值或对象都有一个确切的类型——要么是* `*null*` *、原语，要么是已知的类类型。我们可以调用类似* `*value.GetType()*` *或* `*value.getClass()*` *的方法在运行时查询确切的类型。这种类型的定义将驻留在某个具有某个名称的类中，并且我们不能使用两个具有相似形状的类来代替彼此，除非有显式的继承关系或共同实现的接口。*

*这些方面描述了一个具体化的、名义上的类型系统。我们在代码中编写的类型在运行时存在，并且这些类型通过它们的声明而不是它们的结构相关联。*

它继续以下内容:

*在 C#或 Java 中，认为运行时类型和它们的编译时声明* *一一对应是很有意义的。*

事实上，在 TypeScript 中，所有类型信息都会在运行时丢失。这种一对一的对应是不存在的。这意味着我们不能像在。例如 NET core。更重要的是，**typescript 在运行时不提供任何类型安全。**

如果没有运行时类型，应用程序就会暴露在一个最常见的错误中:I/O 数据与预期的不同。无论是来自 POST 请求的用户数据、来自外部 API 的数据，还是来自数据库的数据，您的应用程序都可能以意想不到的方式崩溃，并且很难找到问题的根源。如何才能预防这些问题？以下是强化运行时类型脚本代码的三种方法。

# 类型验证库

NPM 上有几个库可以验证用户生成的数据。 [JOI](https://joi.dev/) 是我过去用的最多的图书馆，但是[还有其他的](https://www.npmjs.com/search?q=keywords:validation)。

像这样的库依赖于模式来验证数据，通常用于 web 服务器上的后期数据验证。模式可以非常精确，允许像电子邮件和 UUID 这样的事情，允许字符验证，并包括字段和复杂复合字段的可选、最小和最大长度。完美，以确保用户提供了一个有效的电子邮件地址，而不是试图做任何 SQL 注入。

精确的模式意味着错误也可以是描述性的，因此我们可以向服务的用户提供有价值的反馈。

这些库的缺点是在我们的类型之上需要一个单独的模式。这意味着您必须在两个地方维护类型。

文档中的[示例很好地展示了不同的特性。最小和最大长度、模式、整数等。](https://joi.dev/api/?v=17.6.0)

```
const Joi = require('joi');

const schema = Joi.object({
    username: Joi.string()
        .alphanum()
        .min(3)
        .max(30)
        .required(),

    password: Joi.string()
        .pattern(new RegExp('^[a-zA-Z0-9]{3,30}$')),

    repeat_password: Joi.ref('password'),

    access_token: [
        Joi.string(),
        Joi.number()
    ],

    birth_year: Joi.number()
        .integer()
        .min(1900)
        .max(2013),

    email: Joi.string()
        .email({ minDomainSegments: 2, tlds: { allow: ['com', 'net'] } })
})
    .with('username', 'birth_year')
    .xor('password', 'access_token')
    .with('password', 'repeat_password');

schema.validate({ username: 'abc', birth_year: 1994 });
// -> { value: { username: 'abc', birth_year: 1994 } }
```

## 优点:

*   非常详细的输入数据检查包括电子邮件地址的验证
*   非常适合用户生成的表单数据
*   良好的错误处理/报告

## 缺点:

*   类型的重复，因为我们已经在 typescript 中定义了类型

# 使用编译器插件进行运行时类型检查

[TTypescript](https://github.com/cevek/ttypescript)(Transformer Typescript)是一个替代的 TypeScript 编译器，允许在编译 TypeScript 代码的同时执行插件。插件可以处理应用程序中的类型，并将它们编译成具体的运行时代码。我们需要做的就是更新编译器并安装一个 NPM 包来进行类型检查。

TTypeScript 要求我们将编译器从 *tsc* 更新为 *ttsc* 或者添加一个类似`ts-node --compiler ttypescript`的编译器标志。

NPM 包[*TypeScript-is*](https://github.com/woutervh-/typescript-is)*提供基于您现有的类型脚本类型的类型检查，并提供描述性错误。我发现对 express 服务器的所有输出使用 typescript-is 很有帮助。它在单元和集成测试之上提供了额外的信心层。下面是一个直接来自文档的示例:*

```
*import { assertType } from 'typescript-is';

const object: any = 42;
assertType<number>(object).toFixed(2); // "42.00"

try {
    const asString = assertType<string>(object); // throws error: object is not a string
    asString.toUpperCasse(); // never gets here
} catch (error) {
    // ...
}*
```

*在这个例子中，当我们传入的对象不是正确的类型时，函数 assertType 抛出一个错误。这个库的用途不仅限于此，它还可以在 if 语句中用作简单的类型保护。*

*这个库的缺点是我们只能通过简单的类型进行测试，我们不能通过字符串长度、最大数量或验证电子邮件地址或电话号码来测试任何东西。*

## *赞成的意见*

*   *使用现有的 TypeScript 类型*
*   *没有额外的编译步骤*
*   *支持类型保护和类型验证*

## *骗局*

*   *例如，与 JOI 相比，基于原语的类型检查具有有限的特异性。*
*   *需要更新的 TypeScript 编译器*

*如果你想更深入地了解 TypeScript 编译器插件，[这本手册](https://github.com/madou/typescript-transformer-handbook)是一个极好的开始。*

# *打字稿自动防护*

*[](https://github.com/rhys-vdw/ts-auto-guard) [## 从 TypeScript 接口生成类型保护函数

### 从 TypeScript 接口生成类型保护函数一个为…自动生成类型保护的工具

github.com](https://github.com/rhys-vdw/ts-auto-guard) 

这个包与 TypeScript-is 相当，它生成运行时代码来根据 TypeScript 接口定义验证变量。不同之处在于，自动防护使用单独的编译步骤来生成包含类型检查代码的*.guard.ts 文件。

## 赞成的意见

*   使用现有的 TypeScript 类型
*   生成的类型保护被生成并包含在源代码中
*   修改类型保护的可能性

## 骗局

*   例如，与 JOI 相比，类型检查的定义是有限的。
*   需要额外的编译步骤
*   类型定义和保护可能会不同步

感谢您的阅读，希望您对这篇文章感兴趣。请支持我，在媒体上关注我，在 [Twitter](https://twitter.com/laurent_zw) 上关注我，或者在 [LinkedIn](https://www.linkedin.com/in/laurentzuijdwijk/) 上关注我。* 

## *资源*

*[1]打字稿手册[https://www . typescriptlang . org/docs/handbook/TypeScript-in-5-minutes-OOP . html](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-oop.html)*

*[2]https://www.npmjs.com/search?q=keywords:validation NPM 验证库*

*[3]乔伊[https://joi.dev/](https://joi.dev/)*

*[4]t 打字稿[https://github.com/cevek/ttypescript](https://github.com/cevek/ttypescript)*

*[https://github.com/madou/typescript-transformer-handbook](https://github.com/madou/typescript-transformer-handbook)*

*[6]TypeScript decorators[https://www . typescriptlang . org/docs/handbook/decorators . html](https://www.typescriptlang.org/docs/handbook/decorators.html)*

*[7][https://github.com/woutervh-/typescript-is](https://github.com/woutervh-/typescript-is)*

*[8]https://github.com/madou/typescript-transformer-handbook*

**更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。**