# 如何在 React useEffect()挂钩中使用 Async/Await

> 原文：<https://javascript.plainenglish.io/react-useeffect-async-await-478d0ca81330?source=collection_archive---------3----------------------->

## 了解如何在 React useEffect()钩子中的异步函数上轻松使用 await 操作符。

![](img/ad382bdeef0f9ca53e9b18153d54ac9e.png)

对于 React `useEffect()`钩子中的`await`函数，将`async`函数包装在一个立即调用的函数表达式(IIFE)中。

例如:

```
const [books, setBooks] = useState([]);useEffect(() => {
  (async () => {
    try {
      // await async "fetchBooks()" function
      const books = await fetchBooks();
      setBooks(books);
    } catch (err) {
      console.log('Error occured when fetching books');
    }
  })();
}, []);
```

在本文中，我们将看看在`useEffect()`钩子中调用`async`函数的不同方法，以及在使用`async` / `await`时要避免的陷阱。

# 使用 useEffect()中的 then/catch 调用异步函数

`async`函数在 JavaScript 中执行异步操作。为了在 React useEffect()钩子中等待`Promise``async`函数返回被解决(完成或拒绝),我们可以使用它的`then()`和`catch()`方法:

在下面的例子中，我们调用了`fetchBooks()`异步方法来获取和显示样本阅读应用中存储的书籍:

```
export default function App() {
  const [books, setBooks] = useState([]); useEffect(() => {
    // await async "fetchBooks()" function
    fetchBooks()
      .then((books) => {
        setBooks(books);
      })
      .catch(() => {
        console.log('Error occured when fetching books');
      });
  }, []); return (
    <div>
      {books.map((book) => (
        <div>
          <h2>{book.title}</h2>
        </div>
      ))}
    </div>
  );
}
```

# 异步/等待问题:异步回调无法传递给 useEffect()

也许您更喜欢使用`async/await`语法来代替`then/catch`。您可以通过将回调传递给`useEffect()` `async`来尝试这样做。

这不是一个好主意，如果你使用的是棉绒，它会马上通知你。

```
// ❌ Your linter: don't do this!
useEffect(async () => {
  try {
    const books = await fetchBooks();
    setBooks(books);
  } catch {
    console.log('Error occured when fetching books');
  }
}, []);
```

你的 linter 抱怨是因为`useEffect()`的第一个参数应该是一个函数，要么不返回任何东西，要么返回一个函数来清除副作用。但是`async`函数总是返回一个`Promise`(隐式或显式)，并且`Promise`对象不能作为函数调用。这可能会导致 React 应用程序出现真正的问题，比如内存泄漏。

```
useEffect(async () => {
  const observer = () => {
    // do stuff
  }; await fetchData(); observable.subscribe(observer); // Memory leak!
  return () => {
    observable.unsubscribe(observer);
  };
}, []);
```

在这个例子中，因为回调函数是`async`，它实际上并不返回定义的清理函数，而是返回一个用清理函数解析的`Promise`对象。因此，这个清除函数永远不会被调用，观察者永远不会从可观察对象中退订，从而导致内存泄漏。

那么我们该如何解决这个问题呢？如何在`useEffect()`钩子中使用带有`async`功能的`await`操作符？

# async/await 解决方案 1:在 IIFE 中调用异步函数

解决这个问题的一个直接方法是将`async`函数中的`await`函数[立即调用函数表达式](https://developer.mozilla.org/en-US/docs/Glossary/IIFE)(life):

```
const [books, setBooks] = useState([]);useEffect(() => {
  (async () => {
    try {
      const books = await fetchBooks();
      setBooks(books);
    } catch (err) {
      console.log('Error occured when fetching books');
    }
  })();
}, []);
```

顾名思义，生命是一个一旦被定义就运行的函数。它们用于避免污染全局命名空间，以及在尝试一个`await`调用可能导致包含生命的作用域出现问题的场景中(例如在`useEffect()`钩子中)。

# 异步/等待解决方案 2:在命名函数中调用异步函数

或者，您可以在一个命名函数中`await`这个`async`函数:

```
useEffect(() => { // Named function "getBooks"
  async function getBooks() {
    try {
      const books = await fetchBooks();
      setBooks(books);
    } catch (err) {
      console.log('Error occured when fetching books');
    }
  } // Call named function
  getBooks();
}, []);
```

还记得使用可观察模式的例子吗？下面是我们如何使用一个命名的`async`函数来防止发生的内存泄漏:

```
// ✅ callback is not async
useEffect(() => {
  const observer = () => {
    // do stuff
  }; // Named function "fetchDataAndSubscribe"
  async function fetchDataAndSubscribe() {
    await fetchData();
    observable.subscribe(observer);
  } fetchDataAndSubscribe(); // ✅ No memory leak
  return () => {
    observable.unsubscribe(observer);
  };
}, []);
```

# 异步/等待解决方案 3:创建自定义挂钩

我们还可以创建一个自定义钩子，它的行为类似于`useEffect()`，并且可以接受`async`回调而不会导致任何问题。

自定义挂钩可以这样定义:

```
export function useEffectAsync(effect, inputs) {
  useEffect(() => {
    return effect();
  }, inputs);
}
```

我们可以从代码中的多个地方调用它，就像这样:

```
const [books, setBooks] = useState([]);useEffectAsync(async () => {
  try {
    const books = await fetchBooks();
    setBooks(books);
  } catch (err) {
    console.log('Error occured when fetching books');
  }
});
```

有了这三种方法，我们现在可以很容易地在`useEffect()`钩子中使用带有`async`函数的`await`操作符。

*最初发表于*[*codingbeautydev.com*](https://cbdev.link/9c5c72)

# ES13 中 11 个惊人的新 JavaScript 特性

本指南将带您快速了解 ECMAScript 13 中添加的所有最新功能。这些强大的新特性将会用更短、更富于表现力的代码来更新您的 JavaScript。

![](img/75a56482761ab63cfc081ad691d70d61.png)

报名参加，马上就能得到一份免费的。