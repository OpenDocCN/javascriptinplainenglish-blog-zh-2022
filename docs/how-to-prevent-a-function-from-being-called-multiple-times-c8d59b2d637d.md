# 如何防止一个函数被多次调用

> 原文：<https://javascript.plainenglish.io/how-to-prevent-a-function-from-being-called-multiple-times-c8d59b2d637d?source=collection_archive---------6----------------------->

如果你使用一个事件处理程序，比如 **onClick** 、 **onChange、**或者 **onScroll** ，并且想要防止回调被过快地触发，那么你可以限制回调的执行速率。这可以通过以下可能的方式实现。

# 节流

基于基于时间的频率的变化。比如可以用 **_。油门** lodash 功能。

```
_.throttle(func, wait, options)
```

Lodash 的 **_。throttle()** 方法创建一个每毫秒只能调用一次函数参数的 throttled 函数。该方法至少需要两个参数，即函数和节流时间。

# 去抖动

当一个函数被传递给 Lodash 的去抖函数时，它会延迟函数的执行。例如，当我们想要通过键入输入来实现搜索时，它会很有帮助。我们不应该为每个输入的字符调用搜索 API 请求，而应该只在用户停止输入后才调用它。

```
export default function App() {
  const [results, setResults] = React.useState([])

  const debouncedSearch = React.useRef(
    debounce(async () => {
      const response = await fetch(`/api/search?query=${query}`)
      const body = await response.json()
      const results = body.results.map((result) => result.name)
      setResults(results)
    }, 300)
  ).current

  async function handleChange(e) {
    debouncedSearch(e.target.value)
  }

  return (
    <div>
      <input
        type="search"
        placeholder="Enter your search"
        onChange={handleChange}
      />
      <ul>
        {results.map((result) => (
          <li key={result}>{result}</li>
        ))}
      </ul>
    </div>
  )
}
```

在 ReactJS 中使用 Lodash 去反跳方法最好是将其包装在 useRef 函数中，因为这样可以跟踪去反跳函数并防止在每次渲染时创建它们。

# RequestAnimationFrame 节流

当一个函数用于渲染动画或者计算元素的位置时，我们可以使用 RequestAnimationFrame 来防止它被触发太多次。

```
const rafId = requestAnimationFrame(callback);
```

每次浏览器开始下一次绘制页面之前，Windows.requestAnimationFrame 都会执行您的回调(通常每秒 60 次)。要停止它，您需要调用 **cancelAnimationFrame** 并传递请求的 id(示例中的 **rafId** )。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***