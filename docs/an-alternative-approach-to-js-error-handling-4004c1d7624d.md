# JavaScript 错误处理的另一种方法

> 原文：<https://javascript.plainenglish.io/an-alternative-approach-to-js-error-handling-4004c1d7624d?source=collection_archive---------3----------------------->

## 有没有可能在不使用“异常”的情况下实现干净的错误处理？

![](img/e0db240f6b97cd5abbf2b8d3f8b3b08a.png)

鲍勃叔叔是对的。处理错误最干净的方法是使用异常。当然，一个`try-catch`块要比返回错误方便得多。但是这种便利是有代价的:当您`throw`一个异常时，执行在性能方面变得昂贵。在 Node.js 的某些版本中，情况变得更糟，编译器甚至不会优化`try-catch`块。

因此，让我们看看其他选项，并对它们进行改进，直到找到一个可接受的替代方案。

## 1.循着`Golang`的方式

`Go`编程语言有一个内置的`error`类型，它可以和正常结果一起从函数返回:

```
normalResult, err := myFunc()
if err != nil {
  fmt.Println(err)
}
```

使用 javascript 析构特性，我们可以模仿这种行为:

```
const {normalResult, error} = myFunc();
if( error != null ) {
  console.error(`Error occured: ${error}`);
}
```

但是等等！将几个返回错误的函数放在一起会导致`if-chain`地狱:

```
const {normalResult1, error1} = myFunc1();
if( error1 === null ) {
  const {normalResult2, error2} = myFunc2();
  if( error2 === null ) {
    ...
  } else {
    // Handle error2
  }
} else {
  // Handle error1
}
```

加油！太可怕了！

## 2.一次迭代循环

这是过去`C`编程的一个技巧，也可以应用于 JS:

```
do {
  const {normalResult1, error1} = myFunc1();
  if( error1 ) {
    // Handle error1
    break;
  }
  const {normalResult2, error2} = myFunc2();
  if( error2 ) {
    // Handle error2
    break;
  }
} while(false);
```

那好多了。

但是那些`if`是令人生畏的。不是吗？声明几个不同的`error`变量也让人不知所措。

如果有一种方法可以在任何对`myFuncN`的调用之后临时退出循环，检查调用方的结果是否有错误，然后在没有检测到错误的情况下返回到下面的语句，那就太好了。

我说的是带有**多重** *退出点*的特定类型的函数。此外，我希望能够重新进入该功能，但不是从其开始，而是从最后的*退出点*开始。

你猜到了吗？没错！

## 3.满足发电机功能

在 JS 中，使用关键字`function*`定义了一个生成器函数。(注意那个小小的星号！)

```
function* myGeneratorFunc(inValue) {

  yield inValue;  // The first exit point
  yield inValue + 1; // The second (and last) exit point
}
```

我们第一次调用生成器函数时，它返回一个`Generator`对象:

```
const generator = myGeneratorFunc(5);
```

函数体还没有执行。为此，我们在`generator`对象上调用`next()`:

```
console.log(generator.next().value);
// expected output: 5
```

该语句使函数运行到第一个`yield`语句。如果那个`yield`包含一个值，我们可以通过`next().value`访问它。

现在，如果我们再次调用`next()`方法呢？

从上一个`yield`到下一个`yield`恢复功能执行:

```
console.log(generator.next().value);
// expected output: 6
```

你可能会注意到这里的模式。我们需要循环调用`next()`方法。但是有一种优雅的方式可以做到这一点:`Generator`对象符合`Iterator`协议，这意味着我们可以这样写:

```
for( let myValue of myGeneratorFunc(5) ) {
  console.log(myValue);
}
```

酷！

## 4.通用错误处理循环

有了所有的工具，我们可以创建一个通用的错误处理循环:

```
async function **tryRun**(
{
  **try**: inTryGeneratorFunc,
  **catch**: inCatchFunc
},
**inContext**
) {
  if( !inTryGeneratorFunc ) {
    throw new Error('The `tryGeneratorFunc` is required!');
  }
  let resultError = null;
  await (async () => {
    const boundedTryGeneratorFunc =   
           inTryGeneratorFunc.**bind**(inContext);
    for await (let {error} of boundedTryGeneratorFunc()) {
      if( error ) {
        resultError = error;
        if( inCatchFunc ) {
          inCatchFunc(error);
        }
        break;
      }
    }
  })();
  return resultError;
}
```

在深入研究代码之前，让我们看一个简单的用例。假设我们有两个函数返回一个包含`error`字段的对象:

```
function successfulFunc() {
  let result = {
    **error**: null,  // We should have an 'error' field
    data: 'myData1'
  }
  return result;
}
function failingFunc() {
  let result = {
    **error**: 'Something went wrong!',
    data: 'myData2'
  };
  return result;
}
```

现在我们的`tryRun`上场了:

```
await **tryRun**({
  **try**: async **function*** () { // Don't forget '*' !

    yield successfulFunc();
    yield failingFunc();
  },
  **catch**: (inError) => {
    console.error(inError);
    // Handle those two potential errors
  }
});
```

不幸的是，JS 还不支持生成器的箭头函数语法。因此，`try`生成器函数不能访问父块中的上下文。这就是为什么我在`tryRun`函数中包含了一个`inContext`参数。这个参数可以通过可爱的`this`对象在`try`函数中访问。当在类方法中使用`tryRun`函数时，这更明智。没有`inContext`参数，`try`生成器函数不会访问类实例变量或方法！幸运的是，将`this`保存为`that`让我们得到了保护:

```
const **that** = this;
await tryRun({
  try: function* () {
    // Here we can access 'this' as the parent object
  },
  catch: (inError) => {
    console.error( inError);
  },
  **that**);
```

为什么我把函数声明为`async`？它是更一般的。毕竟等一个`sync`函数不吃亏！

我做了一个简单的[库](https://github.com/hayoola/try-run-showcase/tree/main)来演示这项技术的用法。看一看，不要忘记检查单元测试。

脚注:

1.  干净的代码:敏捷软件工艺手册，皮尔森，2018 年

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*