# React-Query 和 SWR 的 5 个妙招

> 原文：<https://javascript.plainenglish.io/five-clever-hacks-for-react-query-or-swr-27c2453f4e2d?source=collection_archive---------1----------------------->

因此，在 React 18 中处理双重渲染问题最终让你使用了像 [react-query](https://react-query.tanstack.com/) 或 [SWR](https://swr.vercel.app/) 这样的 API 处理库。厉害！但是，您知道吗，您可以从 12Kb(或者 SWR 的 4Kb)中获得比 API 抓取更多的东西？以下是这些令人敬畏的库的五种非常新颖的用法。

# 更喜欢视频？

如果你更喜欢看你的技术故事，那就去 YouTube 上看看。

Five Clever Hacks for React-Query and SWR: The Video!

# 简化的多次提取

我们倾向于把一个`useQuery`钩子看作是每次获取一个钩子。但是，假设您要进行两次提取。例如，您有一个登录系统，在该系统中，您首先获取进行登录，然后在获得用户 ID 后再次获取用户信息。

您可能会从以下内容开始:

```
import { useQuery } from "react-query";const fetchLogin = () => fetch("/login.json").json();
const fetchUser = (id) => fetch(`/${id}.json`).json();*const MyComponent = () => {
  const* { *data*: login } = *useQuery*("login"*,* fetchLogin);
  *const* { *data*: user } = *useQuery*(
    "user"*,* () => fetchUser(login.id),
    { enabled: login?.id }
  ); return <div>{JSON.stringify(user)}</div>
}
```

在这个模型中，我们级联这两个`useQuery`钩子。首先，我们获取登录名，然后一旦登录名返回非零的`id`，我们就`enable`进行第二次查询。现在，这是可行的。可是这样的痛苦！想象一下，如果有三个或更多的请求会更复杂。一定有更好的方法！

当然，我们可以只做一个`login`函数，就像这样:

```
const login = async () => {
  const resp = await fetch("/login.json");
  const { id } = await resp.json(); const userResp = await fetch(`/${id}.json`);
  const user = await userResp.json();
  return user;
};
```

在我们的组件中使用它。

```
*const MyComponent = () => {
  const* {data: user} = *useQuery*("login"*,* login);
  return <div>{JSON.stringify(user)}</div>
}
```

你看，`useQuery`监控任何函数，它可以是单个的`fetch`，也可以是这样的函数，用逻辑等进行多次提取。或者它可能根本就不是一个提取(正如我们将很快看到的)。这里的要点是开始跳出`fetch`的框框思考。

但是在我们结束关于`fetch`的话题之前，让我们来看两个更方便的变体。

例如，如果您要进行一系列的读取操作，您可以这样做:

```
const getTextData = async () => {
  const out = [];
  for (const name of ["a", "b", "c"]) {
    const resp = await fetch(`/data_${name}.json`);
    out.push(await resp.json());
  }
  return out;
};
...
*const* {data: textData} = *useQuery*("textData"*,* getTextData);
```

在这种情况下，我们使用一个`for`循环来遍历一个值数组，然后在返回所有值之前请求每个值的 JSON。顺便说一句，如果你喜欢这个例子，但不喜欢`for`，你用`forEach`替换它，它不会工作，那是因为`forEach`与`async/await`不兼容，但是嘿，你自己试试看，享受吧。

如果您想并行执行此操作，可以尝试如下方式:

```
const getTextData = async () => Promise.all(
  ["a", "b", "c"].map(async (name) => {
    const resp = await fetch(`/data_${name}.json`);
    return await resp.json();
  })
);
```

这也是可行的，但是我不认为结果的顺序是有保证的，这将取决于单个读取的解决速度。

我听到你在尖叫:“够了，别玩了！给我看看新的！”好吧好吧。

# 记录时间

让我们用 SWR 做一个秒表。不，我没开玩笑！

我们将从创建一个函子(一个产生函数的函数)开始，这个函子将利用一个知道它被创建的时间的函数。当我们调用它时，它会返回开始时间和当前时间之间的差值，以秒为单位。

```
const createStopwatch = () => {
  const startTime = Date.now();
  return () => {
    return Math.round((Date.now() - startTime) / 1000);
  };
};
```

现在，当我们调用`createStopwatch`时，我们将得到一个知道其开始时间的函数，并给出从那时起经过的时间。我们可以在使用`useSWR`钩子的组件中使用它，就像这样:

```
*import* useSWR *from* "swr";const Stopwatch = () => {
  const stopwatchRef = useRef(createStopwatch());
  const { data } = useSWR("stopwatch", stopwatchRef.current, {
    refreshInterval: 100,
    dedupingInterval: 100,
  }); return <div>Time: {data}</div>;
};
```

我们首先创建一个 ref 来保存这个函数，因为我们使用了`useRef`，这个函数在挂载时只会被调用一次。然后我们在`useSWR`钩子中使用那个函数(通过从`stopwatchRef.current`中获取)，由于`refreshInterval`，钩子每 100 毫秒调用一次那个函数。

就是这样！嘣！秒表！我们使用 SWR 内置的刷新间隔来调用这个同步函数，而不是每 100 毫秒获取数据。

现在，这很酷，但并不实际，让我们尝试一些相关但更实际的东西。

# 监控那些日志！

假设您想要 UI 的一部分来监视日志。日志每 100 毫秒就会更新一次 **lot** 。但是您不希望如此频繁地更新 UI，因为，让我们面对现实吧，日志并不是那么重要。那么我们可以使用 react-query(或 SWR)来降低更新速度吗？我们当然可以！

首先，让我们模拟一个日志:

```
const subscribeToLog = () => {
  let log = [];
  let logIndex = 0; setInterval(() => {
    log.push(`${logIndex}: ${Date.now()}`);
    log = log.slice(-3);
    logIndex++;
  }, 100); return () => log;
};const logListener = subscribeToLog();
```

现在我们有了一个`logListener`全局函数，它返回由 interval 函数不断构建的日志消息。每隔 100 毫秒，该间隔会添加一条新的日志消息，然后将日志缩减到最近的三个事件(只是为了保持较小的显示大小。)

现在，我们使用 react-query 来获取日志，但是每秒钟只能获取一次:

```
import { useQuery } from "react-query";const Logger = () => {
  const { data } = useQuery("log", logListener, {
    refetchInterval: 1000,
  }); return (
    <div>
      {data?.map((line, index) => (
        <div key={line}>{line}</div>
      ))}
    </div>
  );
};
```

在本例中，我们使用`useQuery`钩子每 1000 毫秒(1 秒)轮询一次`logListener`(它返回日志中的最后三项)。这限制了显示，所以我们不会太频繁地更新它。

当然，SWR 电码是非常不同的。你得把`refetchInterval`改成`refreshInterval`再加上那个`dedupingInterval`。这很疯狂，我知道，差别是惊人的。

好的，这确实是 react-query 或 SWR 的不同用法，但是我还有什么呢？获取 GPS 坐标怎么样！

![](img/5a4ed6215e626bed58fb2319ae98f167.png)

Five Clever Hacks for React-Query and SWR image

# 带着 GPS 回家

任何你可以包装在承诺中的东西，你都可以用这些棒极了的库来监控。以获取 GPS 坐标为例。这里我们将浏览器的内置`getCurrentPosition`包装在一个承诺中:

```
const getGPSCoordinates = async () =>
  new Promise((resolve, reject) => {
    navigator.geolocation.getCurrentPosition(
      (position) => {
        resolve({
          latitude: position.coords.latitude,
          longitude: position.coords.longitude,
        });
      },
      (error) => {
        reject(error);
      }
    );
  });
```

然后我们可以称之为…让我选一个…这次是 SWR:

```
import useSWR from "swr";const GPS = () => {
  const { data } = useSWR("gps", getGPSCoordinates);
  return <div>Location: {JSON.stringify(data)}</div>;
};
```

就这样，GPS 坐标在你的组件里。

这里的关键点是。任何可以转换成同步函数或基于承诺的异步函数的东西，都可以与这些库一起工作。**任何事情**。一点也不。

# 与 Web Workers 并行

这让我想到了 [Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers) ，它们是非常方便的代码，可以在页面上的不同线程中运行。举一个简单的例子:

```
export const multiplyNumbers = (a, b) => {
  postMessage({ type: "result", result: a * b });
};
```

这个小家伙能把两个数字相乘，然后传回结果。这么好的小功能！无论如何，我们可以使用 react-query(或 SWR)将它集成到我们的代码中，非常简单。我们首先需要加载它:

```
import worker from "workerize-loader!./worker";const workerInstance = worker();
```

现在我们有了一个使用`workerize-loader` Webpack 加载器加载的 worker 实例。然后，我们可以将它包装在一个基于承诺的函数中，该函数调用它，等待结果，然后用输出解析承诺。

```
const multiplyNumbers = async (args) =>
  new Promise((resolve) => {
    workerInstance.addEventListener("message", (message) => {
      if (message.data.type === "result") {
        resolve(message.data.result);
      }
    }); workerInstance.multiplyNumbers(args.a, args.b);
  });
```

我们所做的就是创建一个承诺，在实例上注册一个监听器，然后进行调用。一旦监听器触发，我们就有了结果。下面是使用这个函数的组件代码，这次使用的是 react-query。

```
import { useMutation } from "react-query";const WebWorker = () => {
  const { data: result, mutate } = useMutation(
    "multiply", multiplyNumbers); const [valueA, setValueA] = useState("10");
  const [valueB, setValueB] = useState("20"); return (
    <div>
      <input
        value={valueA}
        onChange={(evt) => setValueA(evt.target.value)}
      />
      <input
        value={valueB}
        onChange={(evt) => setValueB(evt.target.value)}
      />
      <button onClick={
        () => mutate({ a: valueA, b: valueB })
      }>Multiply</button>
      <div>{result}</div>
    </div>
  );
};
```

在这种情况下，我使用 react-query 中的`useMutation`钩子，因为它在主动执行一些事情，这样更有意义。这很重要，因为你可能会用到这些模式。确保您的查询被建模为`useQuery`，并且可能改变事情的操作使用了`useMutation`钩子。

当然，这对 SWR 没有帮助，也没有突变挂钩，但对 SWR 也有办法做到这一点。

现在，让我们通过回答这个古老的问题，以盛大的方式结束这个话题；如果你有反应查询或 SWR，你需要一个状态管理器吗？

# 内置状态管理器？！？

SWR 和 react-query 都管理缓存，对吗？它们都可以确保，如果您从两个不同的位置访问同一个查询键，您将获得相同的数据。

这意味着您可以使用该缓存来全局存储您想要的数据位，并且当您更新它们时，它们将在它们被“订阅”的任何地方更新。这就像是…一个州经理工作的 80%?

所以我们可以创建一个名为`useSWRGlobalState`的定制钩子来完成这个全局共享的任务，看看吧。

```
import useSWR from "swr";const useSWRGlobalState = (key, initialData) => {
  const { data, mutate } = useSWR(key, () => initialData);
  return [
    data ?? initialData,
    (value) =>
      mutate(value, {
        revalidate: false,
      }),
  ];
};
```

您给这个钩子一个`key`，这是我们一直在使用的查询键，以及您想要的任何初始数据。反过来，它使用`useSWR`和`mutate`函数来获取当前数据。

然后钩子返回一个数组，看起来像是从`useState`返回的。这是一个数组，其中第一项是当前值，第二项是 setter 函数。

setter 函数是神奇的地方。我们调用我们得到的`mutate`函数，并赋予它新的值**，但是**我们告诉 SWR **而不是**重新获取该值。也就是说。设置缓存，但仅此而已。

现在我们可以用一些组件来包装它！

```
const StateEditor = () => {
  const [value, setValue] = useSWRGlobalState("sharedText", ""); return (
    <input value={value}
       onChange={(evt) => setValue(evt.target.value)} />
  );
};const StateViewer = () => {
  const [value] = useSWRGlobalState("sharedText", ""); return <div>{value}</div>;
};const GlobalStateDemo = () => {
  return (
    <div>
      <StateEditor />
      <StateViewer />
    </div>
  );
};
```

这里我们有两个独立的组件，一个编辑状态，即`StateEditor`组件，另一个查看共享状态，即`StateViewer`。当您输入`StateEditor`时，变化会立即显示在`StateViewer`中。

不开玩笑，真的。没有上下文。没有 Redux。没有原子。只有一个小钩子，和你已经拥有的“获取库”。💥很疯狂，对吧？

现在，我真的会用这个吗？在一个可能已经有状态管理器的大型应用程序中，肯定没有。但是如果我需要在我的组件层次结构中共享的只是单一的状态，比如用户 ID 和 JWT，那么是的，我可能会这样做。

顺便说一句，React-Query 也可以做到这一点。

```
const useRQGlobalState = (key, initialData) => [
  useQuery(key, () => initialData, {
    enabled: false,
    initialData,
  }).data ?? initialData,
  (value) => client.setQueryData(key, value),
];
```

这个钩子返回一个数组，就像前面一样，其中数组中的第一项是我们用`useQuery`得到的当前值，然后第二个值是一个 setter 函数，它直接在 react-query 客户机上为查询设置缓存数据。

# 包装它

我希望你已经找到了一个有趣的旅程，通过引入这些令人敬畏的库，你可以从你添加到你的应用程序代码中的千字节中挖掘出更多的价值。他们真的是 React 生态系统的无价之宝。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*