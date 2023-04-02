# TypeScript 中的装饰器概述

> 原文：<https://javascript.plainenglish.io/overview-of-decorators-in-typescript-1384ae222ce9?source=collection_archive---------11----------------------->

![](img/6f1c8a63b9a77d8c47dad52ab16e553b.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 打字稿中的装饰者

装饰器是任何编程语言中非常有用和强大的特性。通过将任何方法、类或属性隔离到另一个父函数中，它允许您更改程序的功能，在这个父函数中，我们将拥有更改行为所需的一切

理解 decorator 的一个简单方法是求解这个表达式`the decorator will run when either my programming begin to run or finished running`,其中 decorator 是你的对象的父对象，但不影响程序的执行，尽管你可以在数据被给定的函数处理后操纵它

## 装饰者的用例

在继续之前，让我们试着理解装饰者的一些用例。一个主要的用例是对一组给定的参数进行任何常规操作，

*   将字段设为只读
*   使字段为事件监听和观察做好准备
*   制作字段枚举器

一些功能使用案例如下

*   字段上的常见验证
*   日志记录功能
*   存储错误信息
*   格式化给定字段
*   对不推荐使用的字段或方法发出警告

不管怎样，你可以发现装饰器对任何类型的应用程序都非常有用。因为它们是编译时间过程，所以我们也可以在前端框架中使用它们

## 实验装饰师

目前，typescript 中的 decorators 是实验性的特性，所以它可能会在未来的版本中出现，直到有一个稳定的版本

# Typescript 中的装饰器类型

装饰类型是由不同类别对象的数量定义的，它们可以通过它们的功能附加到这些类别对象上。因为类、函数、s 和属性在编程语言中都有不同的含义，所以我们可以有把握地说它们是所使用的装饰器的一般类别。另一方面，您也可以用以下方式定义装饰者

*   工厂装饰者(Factory decorator)——当你想为函数或属性的行为向装饰者传递一些附加信息时。`e.g logLevel('info')`
*   **类装饰器** —每当构造函数方法调用时的装饰器。`e.g lastActivity()`
*   **属性装饰者** —设置或获取属性时的装饰者。`e.g formatDate('MM-YY-DDDD')`
*   **方法装饰者** —处理方法及其调用，同时保持其执行顺序。

`e.g requiredAttributes(['email', 'firstname'])`

*   **访问 decorator**—用 decorator 管理任何静态或隐藏的属性。`e.g readonly()`
*   **参数装饰器** —将装饰器作为参数传递给任何函数或另一个装饰器。`e.g func(@formbuilder builder)`

你可以在乔纳森·卡多佐的这篇精彩文章中简单了解所有不同的类型及其例子

[](https://www.digitalocean.com/community/tutorials/how-to-use-decorators-in-typescript#creating-accessor-decorators) [## 如何在 TypeScript | DigitalOcean 中使用 Decorators

### 装饰器是用额外的功能来装饰类成员或类本身的一种方式。本教程涵盖了…

www.digitalocean.com](https://www.digitalocean.com/community/tutorials/how-to-use-decorators-in-typescript#creating-accessor-decorators) 

## 装饰者的几个例子

让我们举几个例子来看看实际情况。我们将从日志示例开始。这里我们创建了一个简单的高阶函数，它将接受装饰者的一般参数

*   目标——装饰器所针对的类、窗口或函数
*   memberName —装饰者所附加的对象的名称
*   描述符—对象的任何元数据。它也将包含对象的定义

为了执行，我们使用`call`来运行方法，同时维护参数，然后将其注销。同样方法的另一个扩展可以是`logCatchError`

```
 const logCatchError = () => {
    return (target: any, memberName: string, descriptor: PropertyDescriptor) => {
        const original = descriptor.value;

        descriptor.value = function (...args: any) {
            try {
              const result = original.call(this, ...args);
              return result;
            } catch(error){
              console.error(error)
            }
        }
    }
} 
```

另一个例子——我们可以说一个名为`sendEmail`的方法需要用户的电子邮件和名字，但是假设电子邮件是一个可选字段，那么我们需要限制用户访问该方法

在方法`requiredField`中，我们需要传递一个属性名列表，我们需要检查这些属性名的值，出于文章的目的，我们只能测试这些字段的假值，如果有任何字段不存在，我们就简单地向用户抛出一个错误

```
function requiredField(names: string[]) {
    return (target: any, memberName: string, descriptor: PropertyDescriptor) => {
        const original = descriptor.value;

        descriptor.value = function (...args: any) {
            if (names.some(key => !target[key])) {
                throw new Error(`${names.join()} fields are required while calling ${memberName}`)
            }
            const result = original.call(this, ...args);
            return result;
        }
    }
}

class User {
    firstName: string = "Jon"
    email: string

    @dateFormat('toISOString')
    dob?: Date

    @minLength(8)
    bio: string;

    constructor(bio: string, email?: string, dob?: Date) {
        this.bio = bio
        this.email = email ?? ''
        this.dob = dob
    }

    @logEverything()
    getFullName(prefix: string) {
        return `${prefix} ${this.firstName} ${this.lastName}`;
    }

    @requiredField(['email', 'firstName'])
    sendMail() {
        console.log('sending email to user')
    }
}
```

在同一个例子中，你还可以看到更多的装饰器，如`minLength`和`dateFormat`它们也可以通过使用属性装饰器如 follow 来实现

```
function minLength(limit: number) {
    return function (target: Object, propertyKey: string) {
        let value: string;
        const getter = function () {
            return value;
        };
        const setter = function (newVal: string) {
            if (newVal.length < limit) {
                throw new Error(`Your ${propertyKey} should be bigger than ${limit} characters`)
            } else {
                value = newVal;
            }
        };
        Object.defineProperty(target, propertyKey, {
            get: getter,
            set: setter
        });
    }
}
```

上述装饰者的观点是，我们没有使用 getter 和 setter，因为我们现在使用的属性装饰者没有方法定义

对于格式，我们需要改变接口，因为我直接调用了日期类方法，但是你可以创建更多的属性

```
 interface setterDate extends Date {
    [key: string]: any
}

function dateFormat(format: string) {
    return function (target: Object, propertyKey: string) {
        let value: setterDate;
        const getter = function () {
            if(!value) return 
            return value[format]();
        };
        const setter = function (newVal: Date) {
            value = newVal
        };
        Object.defineProperty(target, propertyKey, {
            get: getter,
            set: setter
        });
    }
}
```

## 结论

装饰器在任何编程语言中都是一个方便的工具。decorator 有一种模式，允许您在 decorator 中创建公共代码，并在项目中彻底使用它们。

考虑到 TypeScript 仍处于试验阶段，我希望您对如何开始使用它的装饰器有一个简单的想法。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***