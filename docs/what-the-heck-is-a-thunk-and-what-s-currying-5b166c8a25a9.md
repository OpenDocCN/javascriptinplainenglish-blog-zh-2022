# JavaScript 中的“Thunk”和“Currying”到底是什么？

> 原文：<https://javascript.plainenglish.io/what-the-heck-is-a-thunk-and-what-s-currying-5b166c8a25a9?source=collection_archive---------5----------------------->

![](img/a0308b41b4ab2bdd682e72fb62afbe84.png)

## 揭开 Thunks 和 Currying 的神秘面纱 JavaScript 中一些最重要的函数式编程概念！

我敢肯定，当你第一次听说编程中的 **thunks** 或**curry**这样的术语时，你的反应应该是这样的:

![](img/abef492815caa2b487658c0bf9c6983c.png)

好吧，别担心，当我第一次听到这些术语时，我也有同样的感觉，特别是从编程方面，直到我意识到它们有多么有用！

在我们开始之前，这篇博文假设您对 JavaScript 和使用承诺和回调的异步编程有基本的了解。一些关于 JavaScript 函数式编程的知识对于更好地理解这两个概念也很有帮助。对于 JavaScript 中的**函数式编程**，Thunks 和**curry**是非常有用的概念。

让我们更深入地了解这些概念，理解它们是什么，以及如何使用它们！

# 关于 JavaScript 中的`thunks`

我们在 JavaScript 中几乎到处都在使用**回调**，用于各种用例，比如**异步编程**、**监听事件**、**处理错误**等等。Thunks 基本上*扩展了回调*的功能，在 JavaScript 的异步编程中非常有用，尽管它们在某些涉及同步编程的场景中仍然非常有用。

# 什么是`thunk`？

一个 **thunk** 只是一个延迟一个值或一些逻辑的计算的函数。

> 单词“thunk”是一个编程术语，意思是“一段做一些延迟工作的代码”。

我们可以写一个函数体或代码，用于以后执行工作，而不是现在执行一些逻辑。许多使用 React 的人可能知道一个非常棒的简单的库，叫做 redux-thunk，顾名思义，它是基于 thunks 的，在使用 redux 进行状态管理时非常有用。

有两种视角可以使用 thunks: **同步**，和**异步**。

# 同步使用方式`thunks`

让我们来谈谈如何使用**同步 thunk** ，

```
const power = (base, exponent) => {
  return Math.pow(base, exponent);
};

// `power` function is evaluated
// and the result is returned immediately
console.log(power(99, 9)); // 913517247483640800

// This is a thunk
const powerThunk = () => {
  return power(99, 9);
};

// Returns the same result as calling the `power` function
console.log(powerThunk()); // 913517247483640800
```

上面的代码片段`power`是一个简单的函数，它计算一个数的幂并立即返回计算出的值。`powerThunk`是一个**同步 thunk** ，它延迟这个结果直到我们调用它。您可能已经注意到，`powerThunk`在内部使用`power`函数来计算并返回计算出的值。

重要的是，这个 thunk 已经成为某个特定状态的包装器。在这种情况下，这是一个潜在的昂贵操作的结果。这种模式允许我们隐藏计算的内部细节，类似于**面向对象编程**范例的[封装](https://www.sumologic.com/glossary/encapsulation/#:~:text=What%20does%20encapsulation%20mean%3A%20In,in%20the%20form%20of%20classes.)的原理。

现在让我们从异步编程的角度来谈谈如何使用 thunks。

# 异步`thunks`

那么我们如何描述一个**异步 thunk** ？这只是一个简单的函数，除了一个**回调函数**，不需要任何额外的参数。在异步 thunks 的情况下，我们可以引入一个延迟来处理一个同步函数，比如前面例子中的`power`函数，或者用它来处理异步 API 调用。

让我们来看看这两种情况。为了更好地理解这一点，我们可以修改前面的**同步 thunk** 示例。

```
const powerAsync = (base, exponent, callback) => {
  return setTimeout(() => callback(Math.pow(base, exponent)), 1000);
};

// This is an async thunk
const powerAsyncThunk = (callback) => {
  return function () {
    powerAsync(99, 9, callback);
  };
};

// This async thunk now returns a function that 
// can be called later on to calculate power.
const calculatePower = powerAsyncThunk((result) => console.log(result));
calculatePower();
```

在上面的代码片段中，我们将`power`函数修改为`powerAsync`函数，即**使用`setTimeout`伪造一个异步函数**，并带一个附加参数`callback`。现在，我们的异步 thunk `powerAsyncThunk`通过返回一个函数来延迟`powerAsync`函数的执行。这使得它非常有用，因为我们现在可以在以后的代码中随时调用这个由`powerAsyncThunk`返回的函数。

现在，我们来谈谈如何使用**异步 thunks** 来处理**异步 API 调用**。

```
const fetchCurrenciesData = (callback) => {
  fetch("https://cdn.jsdelivr.net/gh/fawazahmed0/currency-api@1/latest/currencies.json")
  .then(res => res.json())
  .then(res => callback(res));
}

// This is an async thunk
const asyncThunk = (callback) => {
  return function () {
    fetchCurrenciesData(callback);
  }
}

// This async thunk now returns a function that 
// can be called later on to fetch data from the API.
const fetchCurrencies = asyncThunk((res) => console.log(res));
fetchCurrencies();
```

`fetchCurrenciesData`函数调用一个 API 来获取不同国家的所有货币，并接受一个`callback`函数作为参数。async thunk `asyncThunk`返回一个函数，以后只要我们想在代码中使用这个函数，就可以从 API 中获取数据。

调用`fetchCurrencies`函数后的数据如下:

```
{
aave: "Aave"
ada: "Cardano"
aed: "United Arab Emirates Dirham"
afn: "Afghan afghani"
algo: "Algorand"
doge: "Dogecoin"
dop: "Dominican peso"
dot: "Dotcoin"
dzd: "Algerian dinar"
egld: "Elrond"
egp: "Egyptian pound"
enj: "Enjin Coin"
eos: "EOS"
ern: "Eritrean nakfa"
etb: "Ethiopian birr"
ils: "Israeli New Shekel"
imp: "CoinIMP"
inj: "Injective"
inr: "Indian rupee"
iqd: "Iraqi dinar"
irr: "Iranian rial"
isk: "Icelandic króna"
jep: "Jersey Pound"
jmd: "Jamaican dollar"
jod: "Jordanian dinar"
jpy: "Japanese yen"
kava: "Kava"
kcs: "Kucoin"
kda: "Kadena"
kes: "Kenyan shilling"
...
} 
```

# `thunks`到底用在哪里？💡

既然你已经学习了很多关于 thunks 的知识，你可能想知道 **thunks** 到底用在哪里。

*   JavaScript 中的**承诺**是基于 **thunks** 的概念，在幕后，它使用 thunks。看看这个[视频](https://youtu.be/EhyuWntGA8s)，它讲述了如何使用 **thunks** 对异步函数调用进行排序。
*   [redux-thunk](https://github.com/reduxjs/redux-thunk) 中间件**内部广泛使用 thunk**。这使我们能够使用带有异步逻辑的 **thunks** ，它可以**与 Redux store 的** `dispatch`和`getState`方法进行交互，以便 React 应用程序使用 **Redux** 进行状态管理。

# 关于 JavaScript 中的 Currying

让我们看看 JavaScript 函数式编程中另一个非常有用的概念。

![](img/0cb5f370613a36ce0c594134f5714997.png)

**Currying** 是一种使用函数的高级技术。它不仅在 JavaScript 中使用，也在其他语言中使用！

# 什么是 Currying？

> ***Currying****是将一个函数从可调用的* `*f(a, b, c)*` *转换为可调用的* `*f(a)(b)(c)*` *的函数转换。*

我们正在**通过**分解**来转换**函数，这样就可以一步一步地调用**函数**，而不是立即用所有的参数调用它。这种技术非常有用，特别是当你不能立刻访问所有需要的参数来执行函数中的逻辑时。

让我们看一个例子来更好地理解这一点。假设，我们创建一个简单的函数`multiplyTwoNos`，将两个 no 相乘并返回计算出的值。

```
const multiplyTwoNos = (no1, no2) => {
  return no1 * no2;
};

console.log(multiplyTwoNos(3, 5)); // 15

// A curried function to multiple two nos
const curriedMultiplyTwoNos = function (no1) {
  return function (no2) {
    return no1 * no2;
  };
};

console.log(curriedMultiplyTwoNos(3)(5)); // 15
```

在上面的代码片段中，`curriedMultiplyTwoNos`是一个使用**curry**将`multiplyTwoNos(3, 5)`函数调用转换成类似于`curriedMultiplyTwoNos(3)(5)`的函数调用。输出基本上是相同的，但是当我们可以访问两个数时，currying**给了我们更多的灵活性来计算两个数的乘积。**

# 高级 Currying 实现

现在，让我们来看看多参数函数的**的**高级实现**。我们将首先创建一个通用的 **currying** 函数，然后使用上面的例子将一些数字相乘并得到计算值。**

```
// A function that takes a callback function `func` 
// that defines the kind of operation that will be curried.const curry = function (func) {
  return function curried (...args) {
    // Ensure that we apply the operation defined by `func` 
    // with the max number of arguments supported by `func`. if(args.length >= func.length) {
      return func.apply(this, args);
    } else {
      // If number of parameters are insufficient to call `func` to 
      // perform the operation, recursively call `curried` with previously passed
      // parameters as well as new parameters. 
      return function (...args2) {
        return curried.apply(this, args.concat(args2));
      }
    }
  }
}
```

上面的代码中发生了很多事情！😅

![](img/b328eb3e816f0aa31dff850d1f2a3f2a.png)

但是，不要因为看到上面的代码而不知所措，它实际上非常简单！让我们用一个例子来看看它是如何工作的，然后我们会正确地理解它。

```
const multiplyThreeNos = (no1, no2, no3) => {
  return no1 * no2 * no3;
};

let curriedMultiplication = curry(multiplyThreeNos);

console.log(curriedMultiplication(4, 5, 6)); // 120, still callable normally
console.log(curriedMultiplication(4)(5, 6)); // 120, currying of 1st arg
console.log(curriedMultiplication(4)(5)(6)); // 120, full currying
```

`curry(func)`调用的结果是包装器`curried`,如下所示:

```
function curried(...args) {
    // Ensure that we apply the operation defined by `func`
    // with the max number of arguments supported by `func`. if (args.length >= func.length) {
      return func.apply(this, args);
    } else {
      // If number of parameters are insufficient to call `func` to
      // perform the operation, recursively call `curried` with previously passed
      // parameters as well as new parameters.
      return function (...args2) {
        return curried.apply(this, args.concat(args2));
      };
    }
  };
```

在上面的代码中，我们使用了一些概念，如 [rest 参数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)、**递归**和[。应用()](https://www.freecodecamp.org/news/understand-call-apply-and-bind-in-javascript-with-examples/)。

基本上有两个代码分支，因为有了`if`语句，其中一个可以在`curried`函数中执行。

*   如果传递给`curried`的参数数量**大于或等于**为`func`定义的参数数量，那么只需将调用传递给`func.apply(this, args);`，它将忽略传递的额外参数(如果有)。
*   否则，如果传递给`curried`的参数数量较少，那么我们通过使用`.concat()`方法，用**先前传递的参数**以及**新的参数**递归调用`curried`，直到`curried`的参数数量不足以满足`func`的定义。

> ***注****:***要求函数要有一个***固定个数的自变量。一个使用 rest 参数的函数，比如* `*f(...args)*` *，不能像上面实现的那样进行编译。***

# **什么时候以及为什么要使用 Currying？💡**

**谄媚对以下情况很有用:**

*   **当您想要创建一个只接收单个参数的函数或者稍后在代码中接收参数的函数时，可以使用 Currying。**
*   **它可用于触发事件侦听器。**

**让我们看看为什么你可能需要使用 Currying 的一些原因:**

*   **Currying 提供了一种方法，可以确保在执行函数的核心逻辑之前，函数接收到所有的参数。**
*   **它将您的职能划分为多个较小的职能，可以处理一项职责。这使得你的函数更纯粹，更不容易出错和产生副作用。**
*   **它在函数式编程范例中用于创建[高阶函数](https://dmitripavlutin.com/javascript-higher-order-functions/)。**

# **结论**

**在这篇博客中，我们学习了 **thunks** 和**curry**，这是 JavaScript 中函数式编程的一些最有用但有点先进的概念。我们详细的讨论了 **thunks** 像什么是 **thunks** ，怎么用，什么时候用，用在什么地方。同样，我们学习了**curring**，如何实现**curring**，**curring**的**高级实现**，以及何时使用。**

**我说的就是这些，非常感谢你们阅读我的博客！🙌我希望这篇博客对你有所帮助，让你深入了解了 thunks 和 T42，以及如何在你的 JavaScript 应用中使用这些非常有用的函数式编程范例的概念。😄**

**在我们结束之前，**

**![](img/5e8dc53a7961479f7531ae1e143f6ab2.png)**

> ***随时联系我:* [*Twitter*](https://twitter.com/DevanshYtweets)[*Linkedin*](https://www.linkedin.com/in/devansu-yadav/)[*GitHub*](https://github.com/Devansu-Yadav)**

***更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***