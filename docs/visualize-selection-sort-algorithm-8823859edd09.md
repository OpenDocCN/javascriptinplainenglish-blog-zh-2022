# 可视化选择排序算法

> 原文：<https://javascript.plainenglish.io/visualize-selection-sort-algorithm-8823859edd09?source=collection_archive---------14----------------------->

我总是着迷于想象一个算法。当我打开罗伯特·塞奇威克写的那本算法书时，很难错过他精美的分步插图，这样你就可以详细研究算法了。你有没有想过把这些插图做成动画，看看每个算法是如何用你自己的输入数据开发的？

![](img/4e44cabc9472209a3f88b6c3b9a7183b.png)

## 选择排序

我们以一个最简单的排序算法为例:找到数组中最小的元素并与第一个位置的一个交换，然后找到下一个最小的元素并与第二个位置的一个交换，继续下去直到数组排序完毕。这种方法被称为**选择排序**。在每个外部循环后绘图将得到以下输出:

```
ASORTINGEXAMPLE
AAORTINGEXSMPLE
AAERTINGOXSMPLE
AAEETINGOXSMPLR
AAEEGINTOXSMPLR
...
```

下面是我们可以快速编写的程序:

```
function sort(arr) {
  for (let i = 0; i < n - 1; i++)
    let m = i
    for (let j = i + 1; j < n; j++) {
      if (arr[j] < arr[m]) m = j
    }
    t = arr[m]; arr[m] = arr[i]; arr[i] = t; 
 **console.log(arr);** 
  }
}
```

算法并不太难写，实现的效率是`O(n^2)`。在每个外部循环的末尾添加一个`console.log`来生成我们的输出。

## 如何制作字母动画？

现在让我们假设我们想要动画它。例如，每次我们交换两个元素时，我们可以期望看到两个元素彼此移动并最终在它们的新位置安顿下来的平稳过渡。

```
 S ->       <- A
 A             S
```

让我们使用 HTML/CSS 来实现它。假设数组中有 14 个字母:

```
<div class="canvas">
  <span class="letter">A</span>
  <span class="letter">S</span>
  <span class="letter">O</span>
  ...
</div>.canvas {
  position: relative;
}
.letter {
  position: absolute;
  left: 0;  ***// different for each letter***
  transition: all 1s ease;
}
```

要将字母`S`移动到不同的位置，我们可以将其`absolute`位置从`32px`设置为`320px`，假设每个字母占据`32px`。为了让动画更流畅，我们可以添加`transition`来让动画有一秒钟的放松感。

## 我们制作什么动画？

好的，HTML 和 CSS 是确保字母在屏幕上移动的基本要素。但是我们需要一种方法来创建与动画帧相关联的状态。然后，我们可以在新位置显示字母，以防状态发生变化。

考虑保存数组内容的`initialArr`:

```
const initialArr = 'asortingexample'.split('')
['a', 's', 'o', ...]
```

我们想问以下问题。如果我们跟踪第一个字母`a`，它会移动到什么位置？同样，如果仔细观察第二个字母`s`，它会移动到什么位置？本质上，我们希望跟踪每个字母的位置。虽然听起来很直观，但当你在研究算法时，这可能是一种非常不同的体验，因为你可以跟踪任何其他东西，大部分时间都是派生的属性。

假设我们使用一个`index`数组来跟踪每个字母的位置。例如，最初，第一个字母的位置是`0`，第二个字母的位置是`1`。但是经过几次移动后，第二个字母可以移动到位置`10`。假设我们知道当前运行的`index`数组，我们可以使用下面的 React 代码显示每个字母:

```
 <div className="canvas">
        {**index**.map((v, i) => (
          <span 
            key={i.toString()}
            className="letter"
            style={{ left: v * 32 }}
          >
            {**initialArr**[i]}
          </span>
        ))}
      </div>
```

我们从 14 个字母开始，以 14 个字母结束，因为它们是唯一的对象(尽管它们可以有重复的符号)。因此，我们不打算改变对象的列表；相反，我们只想算出他们当前的位置，然后乘以 32，就像在`left: v * 32`中一样。

**如何生成头寸？**

好，现在给定一个位置列表，我们可以在屏幕上显示它们。但是谁会给我们每一帧的所有位置呢？当然，这是我们正在研究的算法。让我们在 JavaScript 生成器函数的帮助下创建一个:

```
function* **gen**(array) {
  const arr = [...array]
  const index = arr.map((_, i) => i)
  const n = arr.length

  for (let i = 0; i < n - 1; i++) {
    let m = i
    for (let j = i + 1; j < n; j++) {
      if (arr[j] < arr[m]) {
        m = j
      }
    } ii = index.indexOf(i)
    mm = index.indexOf(m)

    t = index[mm]
    index[mm] = index[ii]
    index[ii] = t

    **yield** { index: [...index] }
  }
};
```

我相信你可以从上面的代码中看到我们的算法。有两个循环，每个内部循环后都有一个交换。这比算法本身要复杂一点，但总体来说是直接翻译。开销是我们想要跟踪每个字母在`index`中的位置，而不是最终排序的数组`arr`。

最重要的一行是`yield { index }`，在这里我们暂停算法并输出`index`。这就是我们如何得到当前状态的。将所有内容放在一起，我们得到以下组件`App`:

```
const App = () => {
  const [index, setIndex] = useState(initialIndex)

  useEffect(() => {
    const g = **gen**(initialArr)
    const h = setInterval(() => {
      const run = g.next()
      if (!run.value) {
        clearInterval(h)
      } else {
        setIndex(index)
      }
    }, 1000)
    return () => { clearInterval(h) }
  }, [])

  return (
    <>
      <div className="canvas">
        {index.map((v, i) => (
          <span 
            key={i.toString()}
            className="letter"
            style={{ left: v * 50 }}
          >
            {initialArr[i]}
          </span>
        ))}
      </div>
    </>
  )
}
```

本质上，我们设置了一个一次性的`useEffect`来运行一个动画循环，一旦`App`被加载，我们首先组装一个生成器`g=gen(initialArr)`。此后，对于每一秒`1000ms`，我们调用`g.next()`来获取下一个位置列表。React 将确保`setIndex(index)`的每次更新都会触发屏幕渲染，以更新所有字母。

## 播放演示

如果您错过了任何细节，请在这里随意体验现场演示。

## 想要更多的动画？

从这一刻起，你要做的只是添加更多的动画元素。例如，在交换之前，我们想首先识别我们正在比较的字母，这个字母是由变量`i`跟踪的。

在这种情况下，我们需要修改生成器函数:

```
function* gen(array) {
  const arr = [...array]
  const index = arr.map((_, i) => i)
  const n = arr.length

  for (let i = 0; i < n - 1; i++) {
    ii = index.indexOf(i)
    **yield { index, ii, mm: -1, action: 'loop' }**
    let m = i
    for (let j = i + 1; j < n; j++) {
      if (arr[j] < arr[m]) {
        m = j
      }
    }
```

我们可以再添加一行输出，谁说我们只能生成一种类型的项目，谁说我们只能生成同一类型的数据。在这里，我们可以通过`ii`跟踪字母的位置。而且我们还把这个动作命名为`loop`。所有这些都可以根据自己的目的进行修改。当我们开始使用这个生成器时，我们可以利用新的数据集做更多的事情:

```
const App = () => {
  const [index, setIndex] = useState(initialIndex)
  const [outterId, setOutterId] = useState(0) 

  useEffect(() => {
    const g = gen(initialArr)
    const h = setInterval(() => {
      const run = g.next()
      if (!run.value) {
        clearInterval(h)
        setOutterId(-1)
      } else {
        const { index, ii, mm, action } = run.value
        if (action === 'loop') {
          setOutterId(ii)
        } else {
          setIndex(index)
        }
      }
    }, 1000)
    return () => { clearInterval(h) }
  }, [])

  return (
    <>
      <div className="canvas">
        {index.map((v, i) => (
          <span 
            key={i.toString()}
            className={
              "letter " +
              (i === outterId ? 'highlight ' : '')
            }
            style={{ left: v * 50 }}
          >
            {initialArr[i]}
          </span>
        ))}
      </div>
    </>
  )
}
```

创建新的状态变量`outterId`来跟踪`ii`位置。如果它匹配任何一个字母，它就会附加一个`highlight` CSS 类，所以你可以用不同的方式显示它。

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) *。*