# 对 TypeScript 中属性装饰器的深入介绍

> 原文：<https://javascript.plainenglish.io/a-deep-introduction-to-property-decorators-in-typescript-8ef011169ec?source=collection_archive---------9----------------------->

## 向 TypeScript 类中的属性添加数据和功能

![](img/ef981499854cc12320f3c32bbd34091e.png)

Image by Author, using logos from corresponding projects

Decorators 允许我们在 TypeScript 中向类或方法添加额外的信息，类似于 Java 中的注释。属性装饰器应用于 TypeScript 中的属性定义，并且可以观察它们。

在本文中，我们将探讨属性装饰器的使用和开发。这些装饰器附加到 TypeScript 类中的属性或字段，它们能够观察到已经为特定的类声明了一个属性。要使用 decorator，必须在 TypeScript 中启用它们，所以请务必[阅读本系列的 decorator 介绍文章](/deep-introduction-to-using-and-implementing-typescript-decorators-a9e876ad0d43)。

实际上，它们看起来像这样:

```
class ContainingClass {

    @Decorator(?? optional parameters)
    name: type;
}
```

本文是系列文章的一部分:

本文是系列文章的一部分:

*   [装修工入门](/deep-introduction-to-using-and-implementing-typescript-decorators-a9e876ad0d43)
*   [类装修工](https://itnext.io/deep-introduction-to-class-decorators-in-typescript-23005ea5d035)
*   **物业装修工** *本条*
*   [访问器装饰器](/typescript-accessor-decorators-in-depth-take-control-over-get-and-set-accessor-methods-8b85c95124f9)
*   [参数装饰器](/introduction-to-parameter-decorators-in-typescript-b0042b5474ed)
*   [方法装饰者](/a-deep-introduction-to-method-decorators-in-typescript-6045d52e10a6)
*   [混合装修工](/implement-hybrid-decorator-functions-in-typescript-f6d24bc5abb0)
*   [反射和带装饰器的反射 API](/using-the-reflection-and-reflection-metadata-apis-with-typescript-decorators-c56ba9c690c7)
*   [使用装饰器和反射元数据在 TypeScript 中进行运行时数据验证](/runtime-data-validation-in-typescript-using-decorators-and-reflection-metadata-3219fdf5dfb5)

# TypeScript 中的属性装饰函数

属性装饰器附加到类定义中的属性上。在 JavaScript 中，属性是与对象相关联的值。最简单的属性只是在对象中声明的一个字段。

属性装饰函数接收两个参数:

1.  静态成员的类的构造函数，或者实例成员的类的原型。
2.  给出属性名称的字符串

这为属性装饰函数定义了一个必需的签名。请注意，我们没有得到指向与属性相关的 PropertyDescriptor 对象的指针。TypeScript 文档解释说这是因为属性如何被实例化的细节。因此，结果是除了观察到以该名称命名的属性存在之外，不能做任何事情。

访问器装饰器接收 PropertyDescriptor 对象。如果您的应用程序需要该对象，那么就专注于使用访问器。

让我们尝试一个简单的类装饰器的例子，它简单地打印给定的数据。

```
function logProperty(target: Object, member: string): any {
    console.log(`PropertyExample logProperty ${target} ${member}`);
}

class PropertyExample {

    @logProperty
    name: string;
}

const pe = new PropertyExample();
if (!pe.hasOwnProperty('name')) {
    console.log(`No property 'name' on pe`);
}
pe.name = "Stanley Steamer";
if (!pe.hasOwnProperty('name')) {
    console.log(`No property 'name' on pe`);
}

console.log(pe);
```

`logProperty`函数实现了属性装饰器所需的签名。

在实验过程中，我们了解到，尽管在这个类中明确定义了`name`属性，但是对`hasOwnProperty`的第一次调用返回了`false`，表明该属性不存在。也就是说，研究这个输出:

```
$ node dist/property.js 
PropertyExample logProperty [object Object] name
No property 'name' on pe
PropertyExample { name: 'Stanley Steamer' }
```

事情是这样的:

1.  输出的第一行来自装饰器内部，显示了我们收到的内容，演示了装饰器函数的执行。
2.  但是下一行输出发生了，因为`pe.hasOwnProperty('name')`返回`false`，表明该属性不存在。`hasOwnProperty`函数是从`Object`类中派生出来的，它指示对象是否具有该名称的属性。
3.  然后代码给`pe.name`赋值。
4.  之后，`hasOwnProperty`表示该属性存在。
5.  属性值由`console.log`打印。

这是不是告诉我们，在数据被分配给属性之前，属性是不存在的？

为了更深入地研究这一点，让我们尝试检索 PropertyDescriptor 对象:

```
function logProperty(target: Object, member: string): any {
    console.log(`PropertyExample logProperty ${target} ${member}`);
}

function GetDescriptor() {
    return (target: Object, member: string) => {
        const prop = Object.getOwnPropertyDescriptor(target, member);
        console.log(`Property ${member} ${prop}`);
    };
}

class Student {

    @GetDescriptor()
    year: number;
}

const stud1 = new Student();
console.log(Object.getOwnPropertyDescriptor(stud1, 'year'));
stud1.year = 2022;
console.log(Object.getOwnPropertyDescriptor(stud1, 'year'));
```

`Object`类有两个函数`getOwnPropertyDescriptor`和`defineProperty`，与属性的 PropertyDescriptor 对象相关。这个脚本在装饰器执行时调用`getOwnPropertyDescriptor`,然后在对象实例创建之后，然后在属性赋值之后。

让我们运行这个脚本:

```
$ npx ts-node lib/properties/descriptor.ts 
Property year undefined
undefined
{ value: 2022, writable: true, enumerable: true, configurable: true }
```

在给属性赋值之前，我们无法获取描述符。这证实了我们之前提出的理论。

TypeScript 文档是这样说的:

> *注意，由于属性装饰器在 TypeScript 中的初始化方式，属性描述符不会作为参数提供给属性装饰器。这是因为在定义原型的成员时，目前没有机制来描述实例属性，也没有方法来观察或修改属性的初始化器。*

换句话说，PropertyDescriptor 函数在 property descriptor 对象存在之前执行。

# 向框架注册属性设置

在 decorator 函数中，我们得到了一个目标对象、属性名以及传递给 decorator 函数的任何参数。我们无法覆盖或修改属性的行为。我们能做的是记录来自装饰器的数据，就像我们在用框架注册一个类的[例子中所做的那样。](https://itnext.io/deep-introduction-to-class-decorators-in-typescript-23005ea5d035)

出于基本原理，考虑数据验证的框架。我们可以将 decorators 附加到描述可接受值的属性上，然后验证框架将使用这些设置来确定一个值是否可接受。

```
const registered = [];

function IntegerRange(min: number, max: number) {
    return (target: Object, member: string) => {
        registered.push({
            target, member,
            operation: {
                op: 'intrange',
                min, max
            }
        });
    }
}

function Matches(matcher: RegExp) {
    return (target: Object, member: string) => {
        registered.push({
            target, member,
            operation: {
                op: 'match',
                matcher
            }
        });
    }
}
```

下面是一对属性装饰工厂函数。第一个记录了一个验证操作，该操作确保值是给定范围内的整数。另一个操作是针对正则表达式的字符串匹配。两者的数据都记录在`registered`数组中。

```
class StudentRecord {

    @IntegerRange(1900, 2050)
    year: number;

    @Matches(/^[a-zA-Z ]+$/)
    name: string;
}

const sr1 = new StudentRecord();

console.log(registered);
```

*StudentRecord* 类正在使用这两个属性。然后我们生成该类的一个实例，并打印出`registered`数组。

在真正的验证框架中，我们会使用反射元数据 API 将这些数据存储到一个属性中。我们将在稍后讨论该 API 时讨论这个问题。

现在，让我们运行应用程序:

```
$ npx ts-node lib/properties/register.ts 
[
  {
    target: {},
    member: 'year',
    operation: { op: 'intrange', min: 1900, max: 2050 }
  },
  {
    target: {},
    member: 'name',
    operation: { op: 'match', matcher: /^[a-zA-Z ]+$/ }
  }
]
```

并且，`registered`数组确实记录了可能对这样一个框架有用的信息。

无论我们是否实例化 StudentRecord 类实例，数组都用这些值填充。注释掉`new StudentRecord`行，然后重新运行脚本，同样的数据被打印出来。

我们已经证明，在另一个地方记录任何我们喜欢的关于房产的数据是非常容易的。在某种框架中，其他功能可以参考这些数据并做一些有用的事情。

# 走进死胡同的路径使用`Object.defineProperty`

其他博客上关于 properties decorator 的几篇教程文章建议使用`Object.defineProperty`来实现运行时数据验证。该建议的缺陷就是我们刚刚演示的 PropertyDescriptor 对象对 properties decorator 函数不可用。我们需要讨论一下使用`defineProperty`的不正确建议。

让我们从装饰函数开始:

```
function ValidRange(min: number, max: number) {
    return (target: Object, member: string) => {
        console.log(`Installing ValidRange on ${member}`);
        let value: number;
        Object.defineProperty(target, member, {
            enumerable: true,
            get: function() {
                console.log("Inside ValidRange get");
                return value;
            },
            set: function(v: number) {
                console.log(`Inside ValidRange set ${v}`);
                if (v < min || v > max) {
                    throw new Error(`Not allowed value ${v}`);
                }
                value = v;
            }
        });
    }
}
```

这个装饰器旨在与一个数字属性一起使用，并在`min`和`max`之间强制一个有效的范围。它用`get` / `set`函数调用`defineProperty`，其中`set`函数强制范围。对于数据存储，函数将值存储在局部变量中。这看起来简单明了，不是吗？

这段代码经过精心设置，以匹配前面提到的其他博客中出现的装饰函数。其中一个博客的底部有评论指出了一个问题。看看你自己能否发现这个错误。

要进行测试，请将以下内容添加到脚本中:

```
class Student {
    @ValidRange(1900, 2050)
    year: number;
}

const stud = new Student();
const stud2 = new Student();

stud.year = 1901;
stud2.year = 1911;
console.log(`stud1 ${stud.year} stud2 ${stud2.year}`);
stud.year = 2030;
console.log(`stud1 ${stud.year} stud2 ${stud2.year}`);
// stud.year = 1899;
// console.log(stud.year);

console.log(`stud1 ${stud.year} stud2 ${stud2.year}`);
stud2.year = 2022;
console.log(`stud1 ${stud.year} stud2 ${stud2.year}`);
stud2.year = 2023;
console.log(`stud1 ${stud.year} stud2 ${stud2.year}`);
```

这定义了一个类，并生成了两个实例。我们给一个或另一个实例赋值，然后打印出这些值。如果您想看到数据验证的运行，注释掉分配`1899`的行，您将看到它抛出一个异常。

相反，让我们继续运行:

```
$ npx ts-node lib/properties/descriptor2.ts 
Installing ValidRange on year
Inside ValidRange set 1901
Inside ValidRange set 1911
Inside ValidRange get
Inside ValidRange get
stud1 1911 stud2 1911
Inside ValidRange set 2030
Inside ValidRange get
Inside ValidRange get
stud1 2030 stud2 2030
Inside ValidRange get
Inside ValidRange get
stud1 2030 stud2 2030
Inside ValidRange set 2022
Inside ValidRange get
Inside ValidRange get
stud1 2022 stud2 2022
Inside ValidRange set 2023
Inside ValidRange get
Inside ValidRange get
stud1 2023 stud2 2023
```

每次设置或检索值时，我们都会打印出来。我们看到`stud1`和`stud2`分别被赋值为`1901`和`1911`，但是当这两个值被打印出来时，它们都是`1911`。无论我们给哪个变量赋值，另一个变量都显示相同的值。

发生什么事了？我们之前要求你指出错误。你做得怎么样？

问题是装饰函数内部的数据存储。在构造类定义时，对于给定的类中的每个属性，该函数只执行一次。该函数不是在每次创建类的实例时执行，而是在创建定义时执行。存储数据的本地变量`value`只创建一次。`instance`的实例在 decorator 函数的堆栈框架内，对于每个类的每个属性只执行一次。

这意味着存储在`value`中的数据在所有使用`@ValidRange`的属性实例之间共享。这是因为当使用`@ValidRange`时，属性的数据存储由装饰器管理，而不是由 JavaScript 管理。

在本例中，我们有一个类 Student，它有一个属性`year`，这个属性用`@ValidRange`装饰。正如我们所展示的，相同的值在`year`的两个实例之间共享。

要验证此行为，请将以下字段添加到 Student 类中:

```
@ValidRange(0, 150)
age: number;
```

我们正在建立由`@ValidRange`管理的另一个属性。我们会遇到同样的数据共享问题吗？`age`的值会和`year`的值一样吗？

进行以下更改:

```
stud.year = 1901;
stud2.year = 1911;
stud.age = 20;
console.log(`stud1 ${stud.year} ${stud.age} stud2 ${stud2.year} ${stud2.age}`);
```

这为一个学生实例中的`age`赋值，然后为两个实例打印`age`。

```
Installing ValidRange on year
Installing ValidRange on age
Inside ValidRange set 1901
Inside ValidRange set 1911
Inside ValidRange set 20
Inside ValidRange get
Inside ValidRange get
Inside ValidRange get
Inside ValidRange get
stud1 1911 20 stud2 1911 20
```

`year`和`age`属性的值彼此不同，但在`Student`实例之间共享。我们只给一个值赋值一次，但是请注意，两个实例打印的是相同的值。

为了进一步演示，生成一个新的学生实例:

```
const stud3 = new Student();
```

然后，不要给该实例分配任何值，而是添加一个`console.log`语句:

```
console.log(`stud3 ${stud3.year} ${stud3.age}`);
```

当脚本执行时，您会看到:

```
stud3 1911 20
```

相同的值显示在`stud3`中，尽管没有分配任何值。

属性的每个实例共享相同的值，就像属性的每个实例一样。这是因为`@ValidRange`管理数据存储，而不是 JavaScript 来做。这背后的原因是使用`Object.defineProperty`的方式不正确。JavaScript 确实给了我们很多搬起石头砸自己脚的工具。

当我阅读其他关于属性装饰者的博客文章时，令人惊讶的是运行时数据验证是多么容易。但是，这些帖子中展示的技术是一条死胡同，因为在实现中有一个主要的缺陷。

在 property decorator 函数执行时，JavaScript 还没有创建 PropertyDescriptor 对象。覆盖该属性描述符的`get` / `set`函数可能会非常有用。创建自己的属性描述符并认为已经达到了运行时数据验证的目标是一种误导。

在我们关于[访问器装饰器](https://techsparx.com/nodejs/typescript/decorators/accessors.html)的文章中，我们展示了一种简单的方法，通过在正确的属性描述符中覆盖`get` / `set`函数来实现运行时数据验证。

# 摘要

我们能够将装饰者附加到属性上。这意味着我们可以记录与每个属性相关的装饰者的信息，然后用这些数据做一些事情。但是，我们无法访问 PropertyDescriptor，也无法使用`get` / `set`函数做任何事情。

原因是当类装饰函数执行时。

如果我们可以覆盖 PropertyDescriptor 中的`get` / `set`方法，有很多可能性。但是，对于属性，在为属性赋值之前，该对象并不存在。

我们注意到访问器装饰函数确实接收到了 PropertyDescriptor 对象。我们将在[对 TypeScript](/typescript-accessor-decorators-in-depth-take-control-over-get-and-set-accessor-methods-8b85c95124f9) 中的访问器装饰器的深入介绍中探讨如何处理这个问题。

我们能够做的是在数据结构中记录装饰者信息。例如，`class-validator`包有类似于`@IsInt`或`@Min`或`@Max`的装饰器来验证属性值。我们知道它必须将这些记录到一个数据结构中，当应用程序调用`validate`函数时，它必须检查这些数据以知道如何验证类实例。

# 关于作者

[***大卫·赫伦***](https://davidherron.com) *:大卫·赫伦是一名作家和软件工程师，专注于技术的明智使用。他对太阳能、风能和电动汽车等清洁能源技术特别感兴趣。David 在硅谷从事了近 30 年的软件工作，从电子邮件系统到视频流，再到 Java 编程语言，他已经出版了几本关于 Node.js 编程和电动汽车的书籍。*

*原载于*[*https://techsparx.com*](https://techsparx.com/nodejs/typescript/decorators/properties.html)*。*

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*