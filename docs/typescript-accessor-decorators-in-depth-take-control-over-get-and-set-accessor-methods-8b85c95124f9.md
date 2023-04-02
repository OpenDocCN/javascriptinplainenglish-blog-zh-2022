# 深入的 TypeScript 访问器装饰器:控制“get”和“set”访问器方法

> 原文：<https://javascript.plainenglish.io/typescript-accessor-decorators-in-depth-take-control-over-get-and-set-accessor-methods-8b85c95124f9?source=collection_archive---------13----------------------->

## 探索访问器装饰器的使用和开发。

![](img/318355d102b8b4b2baa9c4f6f83c3285.png)

Decorators 允许我们在 TypeScript 中向类或方法添加额外的信息，类似于 Java 中的注释。访问器装饰器应用于 TypeScript 中的访问器方法定义，可以观察或修改通过 *get/set* 函数访问的数据。只要小心，它们可以用于高级功能，如运行时数据验证。

在本文中，我们将探索访问器装饰器的使用和开发。一个访问器是`get`或`set`方法，我们通过它使用代码来创建或多或少的属性。也就是说，通常我们对现有属性使用`get`和/或`set`，但是它们也可以与属性分开使用。计算出的值可以通过`get`函数传递，例如，一个圆形对象可以存储半径，而`get area`访问器可以通过计算`PI*R**2`告诉我们圆形的面积。要使用 decorator，必须在 TypeScript 中启用它们，所以请务必[阅读本系列的 decorator 介绍文章](/deep-introduction-to-using-and-implementing-typescript-decorators-a9e876ad0d43)。

访问器装饰器被附加到`get`或`set`方法上，无论哪一个在文本中最先出现，都会影响这两个方法。

实际上，它们看起来像这样:

```
class Example {

    #name: string;

    @Decorator
    set name(n: string) { this.#name = n; }
    get name() { return #name; }

    #width: number;
    #height: number;

    @Decorator
    get area() { return this.#width * this.#height; }
}
```

如果您没有意识到这一点，那么`#fieldName`是 JavaScript 中的一个新特性，TypeScript 也支持它，可以为字段数据提供适当的隐私。这些私有字段只能从类内部访问。

对于`name`,访问器函数与同名的现有属性直接相关。对于`area`，访问函数基于另外两个属性计算其值。这个具体的例子是不完整的，因为`#width`和`#height`不能设置它们的值。

本文是系列文章的一部分:

*   [装修工介绍](/deep-introduction-to-using-and-implementing-typescript-decorators-a9e876ad0d43)
*   [类装修工](https://itnext.io/deep-introduction-to-class-decorators-in-typescript-23005ea5d035)
*   [物业装修工](/a-deep-introduction-to-property-decorators-in-typescript-8ef011169ec)
*   **访问者装饰者** *本文*
*   [参数装饰器](/a-deep-introduction-to-method-decorators-in-typescript-6045d52e10a6)
*   [方法装饰者](/a-deep-introduction-to-method-decorators-in-typescript-6045d52e10a6)
*   [混合装修工](/implement-hybrid-decorator-functions-in-typescript-f6d24bc5abb0)
*   [通过装饰器使用反射和反射 API](/using-the-reflection-and-reflection-metadata-apis-with-typescript-decorators-c56ba9c690c7)

# TypeScript 中的访问器装饰函数

访问器装饰器附加到访问器方法上。访问器可能与同名的属性关联，也可能不关联。

访问器装饰函数接收三个参数:

1.  静态成员的类的构造函数或实例成员的类的原型。
2.  成员的名称。
3.  成员的属性描述符。

这些参数与属性装饰器的参数相同，但是增加了 *PropertyDescriptor* 对象。对于[属性装饰器](/a-deep-introduction-to-property-decorators-in-typescript-8ef011169ec)，我们遇到了一些限制，因为它们不接收这个对象。这使得访问器装饰器在应用程序必须有这个描述符的情况下非常有用。

*属性描述符*的定义如下:

```
interface PropertyDescriptor {
    configurable?: boolean;
    enumerable?: boolean;
    value?: any;
    writable?: boolean;
    get?(): any;
    set?(v: any): void;
}
```

在实现 decorators 时，我们将以几种方式使用这个对象。

# TypeScript 中访问器修饰符的简单示例

让我们从一个简单的例子开始探索，这个例子打印了装饰函数接收到的信息。

```
function LogAccessor(target: Object, propertyKey: string,
                    descriptor: PropertyDescriptor) {

    console.log(`LogAccessor`, {
        target, propertyKey, descriptor
    });
}

class Simple {

    #num: number;

    @LogAccessor
    set num(w: number) { this.#num = w; }
    get num() { return this.#num; }
}
```

访问器装饰器附加到这两个方法之一。不允许向两者都添加装饰器。取而代之的是，您将一个装饰器附加到文档顺序中出现的第一个。

如果您将一个装饰器附加到两者上，您将得到以下错误消息:

```
error TS1207: Decorators cannot be applied to multiple get/set accessors of the same name.
```

所以，不要那么做。

若要测试此代码，请添加以下内容:

```
const s1 = new Simple();
const s2 = new Simple();

s1.num = 1;
s2.num = 1;
console.log(`${s1.num} ${s2.num}`);

s1.num = s1.num + s2.num;
s2.num = s1.num + s2.num;
console.log(`${s1.num} ${s2.num}`);

s1.num = s1.num + s2.num;
s2.num = s1.num + s2.num;
console.log(`${s1.num} ${s2.num}`);

s1.num = s1.num + s2.num;
s2.num = s1.num + s2.num;
console.log(`${s1.num} ${s2.num}`);

s1.num = s1.num + s2.num;
s2.num = s1.num + s2.num;
console.log(`${s1.num} ${s2.num}`);

s1.num = s1.num + s2.num;
s2.num = s1.num + s2.num;
console.log(`${s1.num} ${s2.num}`);
```

我们可以运行它来查看输出:

```
$ npx ts-node lib/accessors/first.ts 
LogAccessor {
  target: {},
  propertyKey: 'num',
  descriptor: {
    get: [Function: get num],
    set: [Function: set num],
    enumerable: false,
    configurable: true
  }
}
1 1
2 3
5 8
13 21
34 55
89 144
```

如果你认识到这里计算的数学序列，那就太棒了。

无论如何，我们看到`target`是一个空对象，而`propertyKey`是属性的名称。`descriptor`包含`get`和`set`功能，标记为`non-enumerable`和`configurable`。`get`和`set`字段的内容是我们在代码中编写的函数。

我们用一个计算的访问函数得到什么描述符对象？为了找到答案，让我们创建一个新的简单示例:

```
function LogAccessor(target: Object,
    propertyKey: string,
    descriptor: PropertyDescriptor) { .. as above }

class Rectangle {
    #width: number;
    #height: number;

    @LogAccessor
    get area() { 
        return this.#width * this.#height;
    }

    constructor(width: number, height: number) {
        this.#width = width;
        this.#height = height;
    }
}

const r1 = new Rectangle(3, 5);
console.log(r1.area);
```

*矩形*类没有名为`area`的属性，并且`get area`函数的值是从`width`和`height`值计算出来的。

运行它，我们得到:

```
$ npx ts-node lib/accessors/rectangle.ts 
LogAccessor {
  target: {},
  propertyKey: 'area',
  descriptor: {
    get: [Function: get area],
    set: undefined,
    enumerable: false,
    configurable: true
  }
}
15
```

在这种情况下，生成的 PropertyDescriptor 只有一个`get`函数，其他方面与前面的示例相同。由于只创建了一个`get`函数，这是意料之中的。

# 监视类中的访问器活动

作为我们可以用 PropertyDescriptor 做什么的第一个探索，让我们实现一个装饰器，它通过访问器打印`get` / `set`活动。

```
function AccessorSpy<T>() {
    return function (target: Object, propertyKey: string,
                    descriptor: PropertyDescriptor) {

        const originals = {
            get: descriptor.get,
            set: descriptor.set
        };
        if (originals.get) {
            descriptor.get = function (): T {
                const ret: T = originals.get.call(this);
                console.log(`AccessorSpy get ${String(propertyKey)}`, ret);
                return ret;
            };
        }
        if (originals.set) {
            descriptor.set = function(newval: T) {
                console.log(`AccessorSpy set ${String(propertyKey)}`, newval);
                originals.set.call(this, newval);
            };
        }
    }
}
```

这是从存储库中的`[decorator-inspectors](https://github.com/robogeek/typescript-decorators-examples/tree/main/decorator-inspectors)`包中复制的。

我们使用泛型语法来传递访问器应该使用的数据类型。这个修饰器可以和任何访问器一起使用，所以我们必须使用正确的数据类型。

我们也尊重现有的访问函数。我们将`set`和`get`都保存到`originals`对象中。然后，对于这两者，我们用一个调用原始函数的函数替换任何现有的函数，然后打印其结果。

这个替换函数要求，当调用原始函数时，`this`具有正确的值。`this`的值必须是调用 getter 或 setter 访问器所针对的对象实例。经过几次变化之后——例如，箭头函数不能作为替换函数使用——这里显示的模式被发现能够正确工作。

内部函数中`this`的值与内部函数相关。但是，`descriptor.get`和`descriptor.set`替换函数，以及`originals.get`和`originals.set`，必须在`this`设置为正确的对象实例的情况下执行。使用`call`方法让我们在为`this`设置值的同时调用一个函数。

要测试这一点:

```
class ToSpy {
    #num: number;

    @AccessorSpy<number>()
    set num(w: number) { this.#num = w; }
    get num() { return this.#num; }

}

const tsp1 = new ToSpy();
const tsp2 = new ToSpy();

tsp1.num = 1;
tsp2.num = 2;
console.log(`${tsp1.num} ${tsp2.num}`);

tsp1.num = tsp1.num + tsp2.num;
tsp2.num = tsp1.num + tsp2.num;
console.log(`${tsp1.num} ${tsp2.num}`);

tsp1.num = tsp1.num + tsp2.num;
tsp2.num = tsp1.num + tsp2.num;
console.log(`${tsp1.num} ${tsp2.num}`);

tsp1.num = tsp1.num + tsp2.num;
tsp2.num = tsp1.num + tsp2.num;
console.log(`${tsp1.num} ${tsp2.num}`);
```

我们希望确定，当我们设置属性的值时，它只影响给定的对象实例，并且每个对象实例都有不同的值。

当执行时，我们得到这个:

```
$ npx ts-node lib/accessors/spy.ts 
AccessorSpy set num 1
AccessorSpy set num 2
AccessorSpy get num 1
AccessorSpy get num 2
1 2
AccessorSpy get num 1
AccessorSpy get num 2
AccessorSpy set num 3
AccessorSpy get num 3
AccessorSpy get num 2
AccessorSpy set num 5
AccessorSpy get num 3
AccessorSpy get num 5
3 5
AccessorSpy get num 3
AccessorSpy get num 5
AccessorSpy set num 8
AccessorSpy get num 8
AccessorSpy get num 5
AccessorSpy set num 13
AccessorSpy get num 8
AccessorSpy get num 13
8 13
AccessorSpy get num 8
AccessorSpy get num 13
AccessorSpy set num 21
AccessorSpy get num 21
AccessorSpy get num 13
AccessorSpy set num 34
AccessorSpy get num 21
AccessorSpy get num 34
21 34
```

事实上，我们可以看到 AccessorSpy 函数为我们提供了一个关于这个对象的`get` / `set`活动的很好的视图。而且，我们看到这两个实例之间的值仍然不同。

# 使用访问器装饰器控制可枚举设置

我们希望将一些访问器视为任何其他属性。到目前为止，PropertyDescriptor 的`enumerable`字段是`false`。但是，如果我们希望访问器返回的值包含在由`for...in`或`for..of`循环扫描的字段中，那该怎么办呢？这意味着将`enumerable`设置为`true`。

```
export function Enumerable(val: boolean) {
    return (target: Object, propertyKey: string,
        descriptor: PropertyDescriptor)  => {

        if (typeof val !== 'undefined') {
            descriptor.enumerable = val;
        }
    }
}

class SetEnumerable {

    #num: number;

    @LogAccessor
    @Enumerable(true)
    @LogAccessor
    @AccessorSpy<number>()
    set num(w: number) { this.#num = w; }
    get num() { return this.#num; }

}

const en1 = new SetEnumerable();

en1.num = 1;
for (let key in en1) {
    console.log(`en1 ${key} ${en1[key]}`);
}
```

好吧，我们可能有点喜欢装修。但是，我们使用我们的工具来打印每个步骤的有用信息。

*可枚举的*装饰器简单地在描述符中设置`enumerable`标志。我们传入`true`或者`false`，很简单。我们在之前和之后都使用了 *LogAccessor* 来确保看到设置被更改。并且，我们使用 *AccessorSpy* 来跟踪`num`访问器上的活动。

然后，我们生成一个实例并设置一个值。实际上,`for..in`循环让我们知道访问器是否是可枚举的。如果是，`num`将作为循环中扫描的一个键出现。

```
$ npx ts-node lib/accessors/enumerable.ts 
LogAccessor {
  target: {},
  propertyKey: 'num',
  descriptor: {
    get: [Function (anonymous)],
    set: [Function (anonymous)],
    enumerable: false,
    configurable: true
  }
}
LogAccessor {
  target: {},
  propertyKey: 'num',
  descriptor: {
    get: [Function (anonymous)],
    set: [Function (anonymous)],
    enumerable: true,
    configurable: true
  }
}
AccessorSpy set num 1
AccessorSpy get num 1
en1 num 1
```

事实上，第二个`LogAccessor`输出显示`enumerable`被设置为`true`。然后，在底部我们看到循环内部的打印输出，表明`num`作为一个键被返回。为了验证这一点，设置`Enumerable(false)`并重新运行脚本以确保当`enumerable`为`false`时不打印最后一行。

# 使用访问器装饰器的简单运行时数据验证

我们刚刚证明的是，一个访问器装饰器可以用我们将在运行时执行的代码覆盖`get` / `set`函数。我们用这个来监视进出房产的数据。

但是，我们可以用这种新发现的力量做更多的事情。也就是说，我们可以实现运行时数据验证。

```
function Validate<T>(validator: Function) {
    return (target: Object, propertyKey: string,
        descriptor: PropertyDescriptor) => {

        const originals = {
            get: descriptor.get,
            set: descriptor.set
        };
        if (originals.set) {
            descriptor.set = function(newval: T) {
                console.log(`Validate set ${String(propertyKey)}`, newval);
                if (validator) {
                    if (!validator(newval)) {
                        throw new Error(`Invalid value for ${propertyKey} -- ${newval}`);
                    }
                }
                originals.set.call(this, newval);
            };
        }
    }
}

class CarSeen {

    #speed: number;

    @Validate<number>((speed: number) => {
        console.log(`Validate speed ${speed}`);
        if (typeof speed !== 'number') return false;
        if (speed < 10 || speed > 65) return false;
        return true;
    })
    set speed(speed) {
        console.log(`set speed ${speed}`);
        this.#speed = speed; }
    get speed() { return this.#speed; }

}
```

*Validate* 是一个装饰器工厂，它接受一个我们将用于验证的函数。在内部函数中，我们只覆盖了`set`访问器。这是因为我们想确保不正确的值永远不会到达这个属性。

在我们的`set`函数中，如果`validator`函数存在，我们称之为提供候选值。如果返回`true`，我们说一切都好，继续调用最初的 setter，否则我们抛出一个错误。

我们在每个地方都添加了`console.log`语句，以确保所有步骤都按预期进行。

要测试它，请将以下内容添加到脚本中:

```
const cs1 = new CarSeen();
cs1.speed = 22;
console.log(cs1.speed);

cs1.speed = 33;
console.log(cs1.speed);

cs1.speed = 44;
console.log(cs1.speed);

cs1.speed = 55;
console.log(cs1.speed);

cs1.speed = 66;
console.log(cs1.speed);
```

当执行时，我们得到这个:

```
$ npx ts-node lib/accessors/validation.ts 
Validate set speed 22
Validate speed 22
set speed 22
22
Validate set speed 33
Validate speed 33
set speed 33
33
Validate set speed 44
Validate speed 44
set speed 44
44
Validate set speed 55
Validate speed 55
set speed 55
55
Validate set speed 66
Validate speed 66
.../simple/lib/accessors/validation.ts:16
                        throw new Error(`Invalid value for ${propertyKey} -- ${newval}`);
                              ^
Error: Invalid value for speed -- 66
```

我们可以设置任何我们想要的速度，直到设置一个超出指定范围的值。

这是运行时数据验证。我们分配了一个无效值，验证装饰器确保防止该值污染属性。跟随消息，你会看到每一步都被执行了。对于我们的无效值，执行了前两步，但是，因为抛出了异常，所以最后一步没有执行。因此，属性的值未被修改。

# 摘要

从创建和使用访问器装饰器，到自动化运行时数据验证的基础，我们已经了解了很多。

因为访问器装饰器给了我们 PropertyDescriptor 对象，所以我们可以做很多事情，只要我们小心地去做。特别是，当更换`get`和`set`功能时，我们必须仔细确保更换功能在`this`设置正确的情况下执行。

这种数据验证的方法是最成熟的。其他数据验证包要求程序员显式编码数据验证。这使得它成为一件很容易忘记去做的事情，对吗？使用这种方法，您可以附加 decorators，然后对属性的每个赋值都运行验证，并且您可以确信疯狂的数据值不会进入任何受保护的属性。

# 关于作者

[***大卫·赫伦***](https://davidherron.com) *:大卫·赫伦是一名作家和软件工程师，专注于技术的明智使用。他对太阳能、风能和电动汽车等清洁能源技术特别感兴趣。David 在硅谷从事了近 30 年的软件工作，从电子邮件系统到视频流，再到 Java 编程语言，他已经出版了几本关于 Node.js 编程和电动汽车的书籍。*

*最初发表于*[*https://techsparx.com*](https://techsparx.com/nodejs/typescript/decorators/accessors.html)*。*

*更多内容请看* [***说白了就是***](http://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。*