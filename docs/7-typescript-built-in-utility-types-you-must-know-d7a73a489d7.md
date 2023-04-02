# 您必须知道的 7 种 TypeScript 内置实用程序类型

> 原文：<https://javascript.plainenglish.io/7-typescript-built-in-utility-types-you-must-know-d7a73a489d7?source=collection_archive---------6----------------------->

## 提高对内置类型的理解。

![](img/6a3712f741f64b7291f52b0a8d5bb185.png)

Image by Author

TypeScript 内置了许多有用的实用工具类型，正确使用它们可以使我们的代码更加健壮和优雅。

本文将选择 7 种典型的实用程序类型并分析它们的源代码，列出那些要点，并在 StackBlitz 上创建一个小示例来帮助您理解(您可以调试它)，所以让我们开始吧！

# 部分

它将传入的`Type`的所有属性设置为可选。其源代码如下:

```
/**
 * Make all properties in T optional
 */
type Partial<T> = {
    [P in keyof T]?: T[P];
};
```

我们来分析一下关键点:

`in`操作符:在 JavaScript 中`in`操作符主要是检查一个属性名是否在一个对象中，在 TypeScript 中主要是缩小潜在类型的范围。

`keyof`操作符:`keyof`操作符接受一个对象类型，并生成其键的字符串或数字联合。

以下 StackBlitz 示例显示了它们的功能:

# 必需的

根据需要设置传入`Type`的所有属性。其源代码如下:

```
/**
 * Make all properties in T required
 */
type Required<T> = {
    [P in keyof T]-?: T[P];
};
```

是`Partial<Type>`的反义词。两者对比，发现只多了一个`-`修饰语，可以理解为“减”。

# 只读

它将传入`Type`的所有属性设置为`readonly`。其源代码如下:

```
/**
 * Make all properties in T readonly
 */
type Readonly<T> = {
    readonly [P in keyof T]: T[P];
};
```

可以看到只添加了`readonly`修改器。

能不能根据上一节说的`-`描述符做一个“OnlyChanged”？

# 记录

从属性键`Keys`和属性值`Type`构造一个对象类型。其源代码如下:

```
/**
 * Construct a type with a set of properties K of type T
 */
type Record<K extends keyof any, T> = {
    [P in K]: T;
};
```

我们来分析一下关键点:

`extends`关键字:此处表示限额 K 必须可分配给`keyof any`。

`keyof any`:返回任何可以作为对象索引的值的类型。为什么这么说？这是因为 TypeScript 编译选项中只有[**key of strings only**](https://www.typescriptlang.org/tsconfig#keyofStringsOnly)，默认为 false，那么`keyof any`将返回`string | number | symbol`类型，为 true 时，`keyof any`将返回类型`string`。

# 选择

从“类型”中选择一组属性键来构造新类型。其源代码如下:

```
/**
 * From T, pick a set of properties whose keys are in the union K
 */
type Pick<T, K extends keyof T> = {
    [P in K]: T[P];
};
```

它与上面的`Record<Keys, Type>`非常相似，除了它将传递的联合`K`限定为 T 的所有属性的联合类型，并使用`T[P]`来访问相应的属性值。

# 排除<uniontype excludedmembers="">、提取<type union="">、不可空</type></uniontype>

我把这三个放在一起，因为它们很相似，理解其中一个，剩下的就容易了。

`Exclude<UnionType, ExcludedMembers>`:通过从`UnionType`中排除所有可赋给`ExcludedMembers`的联合成员来构造类型。

`Extract<Type, Union>`:通过从`Type`中提取所有可分配给`Union`的联合成员来构造类型。

`NonNullable<Type>`:通过从`Type`中排除`null`和`undefined`来构造类型。

```
/**
 * Exclude from T those types that are assignable to U
 */
type Exclude<T, U> = T extends U ? never : T;/**
 * Extract from T those types that are assignable to U
 */
type Extract<T, U> = T extends U ? T : never;/**
 * Exclude null and undefined from T
 */
type NonNullable<T> = T extends null | undefined ? never : T;
```

从源代码可以看出，它们的逻辑很简单，如果前者可以赋给后者，那么就设置为`never`类型或者原类型。

这里`never`表示永远不会出现的值的类型，在这里可以用来删除选中的类型。

关于 TypeScript 中`never`类型的秘密，请查看我的另一篇文章:

[](https://blog.bitsrc.io/secrets-of-never-types-in-typescript-de57795a34da) [## TypeScript 中“从不”类型的秘密

### 如何在 TypeScript 中获取 never 类型的值，never vs. void 在 TypeScript 中，never 在 TypeScript 函数声明中。

blog.bitsrc.io](https://blog.bitsrc.io/secrets-of-never-types-in-typescript-de57795a34da) 

# 省略

通过从`Type`中选取所有属性，然后移除`Keys`(字符串文字或字符串文字的联合)来构造类型。其源代码如下:

```
/**
 * Construct a type with the properties of T except for those in type K.
 */
type Omit<T, K extends keyof any> = Pick<T, Exclude<keyof T, K>>;
```

可以看出，它结合了之前介绍的实用程序类型，最终实现了更强大的功能。

今天就到这里。我是 Zachary，我将继续输出与 web 开发相关的故事。如果你喜欢这样的故事，想支持我，请考虑成为 [*中等会员*](https://medium.com/@islizeqiang/membership) *。每月 5 美元，你可以无限制地访问媒体内容。如果你通过* [*我的链接*](https://medium.com/@islizeqiang/membership) *报名，我会得到一点佣金。*

你的支持对我来说很重要——谢谢。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*