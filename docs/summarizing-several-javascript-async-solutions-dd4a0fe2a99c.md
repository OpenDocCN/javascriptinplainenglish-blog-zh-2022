# 总结几种 JavaScript 异步解决方案

> 原文：<https://javascript.plainenglish.io/summarizing-several-javascript-async-solutions-dd4a0fe2a99c?source=collection_archive---------11----------------------->

## JavaScript 异步解决方案

![](img/e44a6425d508fe61d217c7301549138f.png)

## 1.回收

回调简单地理解为一个函数作为参数传递给另一个函数。回调是早期最常用的异步解决方案之一。

回调不一定是异步的，也不直接相关。

举个简单的例子:

```
function f1(cb) {
  setTimeout(() => {
    cb && cb();
  }, 2000);
}

f1(() => {
  console.log("1");
});
```

如上，我们使用 setTimeout 模拟函数 f1 中的一个任务，该任务占用 2s，在耗时任务结束时抛出一个回调，这样我们就可以调用它，使得回调函数在函数 f1 中耗时任务结束时执行。这样，我们就把同步操作变成了异步操作。f1 不会阻塞程序，相当于先执行程序的主逻辑，推迟执行耗时的操作。

**回调利弊**

优点:简单，易懂。

缺点:代码不雅，可读性差，不易维护，高度耦合，层层嵌套造成回调地狱。

## 2.事件监听(发布-订阅模式)

发布-订阅模式定义了对象之间的一对多依赖关系，这样当一个对象的状态改变时，所有依赖于它的对象都会得到通知。

我们都使用过发布-订阅模式，例如，如果我们将一个事件函数绑定到一个 DOM 节点。

```
document.body.addEventListener('click', function () {
  console.log('click');
})
```

但这只是发布-订阅模式最简单的应用，在许多场景中，我们经常使用一些自定义事件来满足我们的需求。

有许多方法可以实现发布-订阅模式，所以这里有一个使用 class 的简单实现。

```
class Emitter {
  constructor() {
    // _listener array, key is the custom event name, value is the execution callback array - as there may be more than one
    this._listener = []
  }

  // 订阅 监听事件
  on(type, fn) {
    // Determine if the event exists in the _listener array.
    // Exists to push the callback to the value array corresponding to the event name, does not exist to add directly
    this._listener[type] 
      ? this._listener[type].push(fn) 
     : (this._listener[type] = [fn])
  }

  // Publish Trigger Event
  trigger(type, ...rest) {
    // Determine if the trigger event exists
    if (!this._listener[type]) return
    // Iterate through the array of callbacks executing the event and pass the parameters
    this._listener[type].forEach(callback => callback(...rest))
  }
}
```

如上所示，我们使用下面的代码创建了一个发射器类，并在和 trigger 上添加了两个原型方法。

```
// Create an emitter instance
const emitter = new Emitter()

emitter.on("done", function(arg1, arg2) {
  console.log(arg1, arg2)
})

emitter.on("done", function(arg1, arg2) {
  console.log(arg2, arg1)
})

function fn1() {
  console.log('I am the main program')
  setTimeout(() => {
    emitter.trigger("done", "Asynchronous parameter I", "Asynchronous parameter II")
  }, 1000)
}

fn1()
```

我们先创建一个发射器实例，然后注册事件，再触发事件，这样也解决了异步问题。

**事件聆听的利弊**

优点:它更符合模块化的思想，我们可以在编写自己的监听器时做很多优化，以便更好地监控程序的运行。

缺点:整个程序变成事件驱动，流程或多或少受到影响，每次使用都要注册事件监听器再触发，相当麻烦，代码也不是很优雅。

## 3.承诺

ES6 标准化并引入了 Promise 对象，这是一个异步编程的解决方案。

简单来说就是用同步的方式写异步代码，可以用来解决回调地狱问题。

许诺对象的状态一旦发生变化，就不会再发生变化，只有两种可能的变化。

> 1.已从待定更改为已解决。
> 
> 2.已从待定更改为已拒绝。

我们使用 setTimeout 来模拟异步操作。

```
function analogAsync(n) {
  return new Promise((resolve) => {
    setTimeout(() => resolve(n + 500), n);
  });
}

function fn1(n) {
  console.log(`step1 with ${n}`);
  return analogAsync(n);
}

function fn2(n) {
  console.log(`step2 with ${n}`);
  return analogAsync(n);
}

function fn3(n) {
  console.log(`step3 with ${n}`);
  return analogAsync(n);
}
```

用承诺去实现。

```
function fn() {
  let time1 = 0;
  fn1(time1)
    .then((time2) => fn2(time2))
    .then((time3) => fn3(time3))
    .then((res) => {
      console.log(`result is ${res}`);
    });
}

fn();
```

**承诺优缺点**

优点:Promise 以同步方式编写异步代码，避免了多层嵌套回调函数，可读性更好。链式操作，可以在 then 中继续写 Promise 对象并返回，然后继续调用 then 进行回调操作。
缺点:承诺对象一旦创建就立即执行，中途不能取消。如果没有设置回调函数，Promise 会在内部抛出错误，不会对外流动。

## 4.发电机

生成器实际上是一个函数，但它是一个特殊的函数。发电机的特别之处在于它可以中途停止。

```
function *generatorFn() {
  console.log("a");
  yield '1';
  console.log("b");
  yield '2'; 
  console.log("c");
  return '3';
}

let it = generatorFn();
it.next();
it.next();
it.next();
it.next();
```

上面的例子是一个具有以下特征的生成器函数。

*   与普通函数不同，生成器函数在函数后和函数名前有一个*
*   该函数有一个内部`yield` 字段
*   调用后函数的返回值使用`next` 方法。

**发电机优缺点**

**优点**:优雅的流量控制方式，允许中断执行功能。

**缺点**:生成器函数的执行必须依赖执行器，只做异步处理还是不太方便。

## 5.异步/等待

ES2017 标准引入了异步功能，使异步操作更加方便。async 的意思是异步，await 是 async wait 的简写，也就是异步等待。async/await 被许多人认为是 js 中异步操作的终极和最优雅的解决方案。

`async` 在做什么？

异步函数返回一个 Promise 对象。如果在 async 函数中直接返回直接数量，async 将通过 Promise.resolve()将直接数量包装在 Promise 对象中。

`await`，还在等什么？

await 是一个表达式，它的计算结果是一个 Promise 对象或其他值(换句话说，没有任何特殊限定)。

*   如果 await 后面没有 Promise 对象，它将被直接执行
*   如果 await 后面跟着一个 Promise 对象，它会阻塞后面的代码，Promise 对象解析，然后获取 resolve 的值作为 await 表达式的结果。
*   await 只能在异步函数中使用

上面用 setTimeout 模拟异步操作，我们用 async/await 来实现。

```
async function fn() {
  let time1 = 0;
  let time2 = await fn1(time1);
  let time3 = await fn2(time2);
  let res = await fn3(time3);
  console.log(`result is ${res}`);
}

fn();
```

输出与上面的 Promise 实现相同，但是 async/await 代码结构看起来更清晰，几乎与同步编写一样优雅。

**异步/等待优缺点**

**优点**:内置执行器，语义更好，适用性更广

**缺点**:误用 await 可能会导致性能问题，因为 await 会阻塞代码。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。*

*报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

*****对缩放您的软件启动感兴趣*** *？检查* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。***