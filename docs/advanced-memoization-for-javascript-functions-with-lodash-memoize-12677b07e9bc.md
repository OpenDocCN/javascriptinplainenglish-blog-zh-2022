# 使用 Lodash.memoize 实现高级 JavaScript 记忆

> 原文：<https://javascript.plainenglish.io/advanced-memoization-for-javascript-functions-with-lodash-memoize-12677b07e9bc?source=collection_archive---------4----------------------->

![](img/facac2b6edf1ee8e2a518de466ce4b7f.png)

Copyright JS Foundation and other contributors

在计算中，记忆化是一种优化技术，主要用于通过存储昂贵的函数调用的结果并在相同的输入再次出现时返回缓存的结果来加速计算机程序—关于记忆的维基百科

[Lodash](https://lodash.com/) 是一个现代的 JavaScript 实用程序库，提供模块化和额外的性能。它是一个无处不在的库，你的项目可能会用到它，即使你没有意识到。Lodash 包含一个以 [memoize](https://lodash.com/docs/4.17.15#memoize) 函数形式的内存化实现。

默认情况下，memoize 函数只使用提供给 memoized 函数的第一个参数作为缓存键。这是记忆化最简单的例子:

```
**const** { memoize } **=** require('lodash');

**const** func **=** (arg1) **=>** `My name is ${arg1}`
**const** funcM **=** memoize(func);

console.dir(funcM('John')); *// => 'My name is John'*
console.dir(funcM('John')); *// => 'My name is John' (cache hit)*
console.dir(funcM.cache.size); *// => 1*
```

重要的是要认识到内存化函数的缓存键是使用 [SameValueZero](https://tc39.es/ecma262/multipage/abstract-operations.html#sec-samevaluezero) 比较来确定的:

```
**const** { memoize } **=** require('lodash');

**const** func **=** (arg1) **=>** JSON.stringify(arg1)
**const** funcM **=** memoize(func);

console.dir(funcM({a: 1})); *// => '{"a":1}'*
console.dir(funcM({a: 1})); *// => '{"a":1}'*
console.dir(funcM.cache.size); *// => 2*
```

现在，如果我们在函数中引入更多的参数呢？

```
**const** { memoize } **=** require('lodash');

**const** func **=** (arg1, arg2) **=>** `${arg1} ${arg2}`;
**const** funcM **=** memoize(func);

console.dir(funcM('John', 'Doe')); *// => "John Doe"*
console.dir(funcM('John', 'FooBar')); *// => "John Doe" (cache hit)*
console.dir(funcM.cache.size); *// => 2*
```

我们可以看到有一个明显的问题。如上所述，lodash 只使用第一个参数作为缓存键。要解决这个问题，我们必须使用解析函数:

```
**const** { memoize } **=** require('lodash');

**const** func **=** (arg1, arg2) **=>** `${arg1} ${arg2}`;
**const** resolver **=** (arg1, arg2) **=>** JSON.stringify([arg1, arg2]);
**const** funcM **=** memoize(func, resolver);

console.dir(funcM('John', 'Doe')); *// => "John Doe"*
console.dir(funcM('John', 'FooBar')); *// => "John FooBar"*
console.dir(funcM.cache.size); *// => 2*
```

这种解析器解决方案显然无法扩展。如果我们的 func 需要消耗复杂对象作为参数怎么办？这很好，除非对象参数很大或者包含循环引用。

当参数是巨大的对象时，我们将花费太多的 CPU 时间将这些对象序列化成 JSON 字符串来确定缓存键。我们将比较巨大的字符串，而不是对象的 SameValueZero 比较。当对象参数包含循环引用时，我们将无法将它们序列化为 JSON 字符串并确定缓存键。

Lodash 还有一招可以克服这两个问题——能够影响缓存键的维护方式。为了实现我们的目标，我们必须创建 lodash.memoize 的专门化；名为 memoizeN 的函数:

```
**const** { memoize } **from** "lodash";

**const** sameValueZero **=** (x, y) **=>** x **===** y **||** (Number.isNaN(x) **&&** Number.isNaN(y));
**const** shallowArrayEquals **=** (a) **=>** (b) **=>** {
  **return** Array.isArray(a) **&&** Array.isArray(b)
    **&&** a.length **===** b.length
    **&&** a.every((val, index) **=>** sameValueZero(val, b[index]));
};
**const** list **=** (...args) **=>** args;

**class** Cache **extends** Map {
  **delete**(key) {
    **const** keys **=** Array.**from**(**this**.keys());
    **const** foundKey **=** keys.find(shallowArrayEquals(key));
    **return** **super**.**delete**(foundKey);
  }
  **get**(key) {
    **const** keys **=** Array.**from**(**this**.keys());
    **const** foundKey **=** keys.find(shallowArrayEquals(key));
    **return** **super**.**get**(foundKey);
  }
  has(key) {
    **const** keys **=** Array.**from**(**this**.keys());
    **return** keys.findIndex(shallowArrayEquals(key)) **!==** **-**1;
  }
}

**const** memoizeN **=** (fn, { resolver **=** list } **=** {}) **=>** {
  **const** { Cache: OriginalCache } **=** memoize;
  memoize.Cache **=** Cache;
  **const** memoized **=** memoize(fn, resolver);
  memoize.Cache **=** OriginalCache;
  **return** memoized;
};
```

这里真正的技巧是，记忆化的函数参数被转换成一个列表，这个列表形成一个缓存键。我们在特定的基础上覆盖 lodash.memoize.Cache 类，我们的实现能够为我们的列表缓存键进行缓存键查找。

观察下面的例子:

```
**const** complexObj **=** {a: 1};
**const** simpleObj **=** {b: 2};

**const** func **=** (arg1, arg2) **=>** arg2;
**const** resolver **=** (arg1, arg2) **=>** [arg1, JSON.stringify(arg2)];
**const** funcM **=** memoizeN(func, { resolver });

console.dir(funcM(complexObj, simpleObj)); *// => {b: 2}*
console.dir(funcM(complexObj, {b: 2})); *// => {b: 2} (cache hit)*
console.dir(funcM({a: 1}, {b: 2})); *// => {b: 2}*
console.dir(funcM.cache.size); *// => 2*
```

我们打算使用这两个参数来构成缓存键，以此来记忆 func。对于第一个参数，对原始值使用 SameValueZero 比较。对于第二种情况，对 JSON 字符串化值使用 SameValueZero 比较。

我们可以进一步专门化，让 memoizeN 使用应用于适当参数的比较器函数列表，而不是滥用解析器来序列化一些参数。

实现将如下所示:

```
**const** memoize **=** require('lodash/memoize');
**const** isEqual **=** require('lodash/isEqual');

**const** sameValueZero **=** (x, y) **=>** x **===** y **||** (Number.isNaN(x) **&&** Number.isNaN(y));
**const** makeShallowArrayEquals **=** (comparators) **=>** (a) **=>** (b) **=>** {
  **return** Array.isArray(a) **&&** Array.isArray(b)
    **&&** a.length **===** b.length
    **&&** a.every((val, index) **=>** {
      **const** comparator **=** **typeof** comparators **===** 'function' ? comparators : comparators[index] **||** sameValueZero;
      **return** comparator(val, b[index]);
    });
};
**const** list **=** (...args) **=>** args;

**class** Cache **extends** Map {
  shallowArrayEquals **=** makeShallowArrayEquals(sameValueZero);

  **delete**(key) {
    **const** keys **=** Array.**from**(**this**.keys());
    **const** foundKey **=** keys.find(**this**.shallowArrayEquals(key));
    **return** **super**.**delete**(foundKey);
  }
  **get**(key) {
    **const** keys **=** Array.**from**(**this**.keys());
    **const** foundKey **=** keys.find(**this**.shallowArrayEquals(key));
    **return** **super**.**get**(foundKey);
  }
  has(key) {
    **const** keys **=** Array.**from**(**this**.keys());
    **return** keys.findIndex(**this**.shallowArrayEquals(key)) **!==** **-**1;
  }
}

**const** memoizeN **=** (fn, { resolver **=** list, comparators **=** sameValueZero }) **=>** {
  **const** { Cache: OriginalCache } **=** memoize;
  memoize.Cache **=** Cache;
  **const** memoized **=** memoize(fn, resolver **||** list);
  memoized.cache.shallowArrayEquals **=** makeShallowArrayEquals(comparators);
  memoize.Cache **=** OriginalCache;
  **return** memoized;
};

module.exports **=** memoizeN;
```

这个版本的 memoizeN 为每个参数应用特定的比较器算法:

```
**const** obj1 **=** {a: 1};
**const** obj2 **=** {b: 2};
**const** obj3 **=** {c: 3};

**const** func **=** (arg1, arg2, arg3) **=>** arg3;
**const** strictEquality **=** (x, y) **=>** x **===** y;
**const** sameValueZero **=** (x, y) **=>** x **===** y **||** (Number.isNaN(x) **&&** Number.isNaN(y));
**const** deepEquality **=** lodash.isEqual;
**const** comparators **=** [strictEquality, sameValueZero, deepEquality];
**const** funcM **=** memoizeN(func, { comparators });

console.dir(funcM(obj1, obj2, obj3)); *// => {c: 3}*
console.dir(funcM(obj1, obj2, {c: 3})); *// => {c: 3} (cache hit)*
console.dir(funcM(obj1, {b: 2}, obj3); *// => {c: 3}*
console.dir(funcM.cache.size); *// => 2*
```

如果我们将 comparators 选项定义为一个函数，那么 memoized 函数将使用它来比较每个参数。当没有提供比较器时，SameValueZero 比较用于所有参数。

```
**const** obj1 **=** {a: 1};
**const** obj2 **=** {b: 2};
**const** obj3 **=** {c: 3};

**const** func **=** (arg1, arg2, arg3) **=>** arg3;
**const** sameValueZero **=** (x, y) **=>** x **===** y **||** (Number.isNaN(x) **&&** Number.isNaN(y));
**const** funcM **=** memoizeN(func, { comparators: sameValueZero }); *// equivalen with memoizeN(func)*

console.dir(funcM(obj1, obj2, obj3)); *// => {c: 3}*
console.dir(funcM(obj1, obj2, obj3)); *// => {c: 3} // cache hit*
console.dir(funcM.cache.size); *// => 1*
```

我已经将 memoizeN 提取到可通过 npm 安装的 [GitHub Gist](https://gist.github.com/char0n/2e6c77d38cf00faacceaf37e46b76a32) 中。如果您更喜欢使用 memoizeN 作为 npm 包，以下是实现方法:

```
$ npm install gist:2e6c77d38cf00faacceaf37e46b76a32 --save
```

此命令将在您的依赖项中创建以下条目:

```
"dependencies": {
  "@char0n/memoizeN": "gist:2e6c77d38cf00faacceaf37e46b76a32" 
}
```

然后通过 CommonJS 或 ESM 使用它:

```
const memoizeN = require('@char0n/memoizeN');
// or
import memoizeN from '@char0n/memoizeN';
```

memoizeN

如果你需要更高级的功能，比如 LRU 缓存、TTL、引用计数等等，我建议你看看 [memoizee](https://github.com/medikoo/memoizee) 。memizee 可能是 JavaScript 中功能最丰富的 memoization 实现。

*原载于*[***https://vladimirgorej.com***](https://vladimirgorej.com/blog/advanced-memoization-for-javascript-functions-with-lodash-memoize/)*2022 年 2 月 5 日*

*更多内容看* [***说白了就是***](http://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。*