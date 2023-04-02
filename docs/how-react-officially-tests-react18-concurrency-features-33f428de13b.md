# React 如何正式测试 React18 并发特性

> 原文：<https://javascript.plainenglish.io/how-react-officially-tests-react18-concurrency-features-33f428de13b?source=collection_archive---------13----------------------->

## 下面是 React 团队如何测试并发特性。

React18 已经在你的雷达上有一段时间了，但是你试过“并发特性”吗？

![](img/ef525f2540eeab7cc9d3b71c806af946.png)

Photo by [Arthur Hickinbotham](https://unsplash.com/@arthurhick?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

当启用并发时，对从“同步更新”到“异步、优先、可中断更新”的变化做出反应。这也使得编写单元测试有点困难。在本文中，我们将讨论 React 团队如何测试并发特性。

**困境**
面临两个主要问题:

## 1.渲染结果怎么表达？

React 可以与来自各种主机环境的渲染器进行通信。最熟悉的渲染器是 ReactDOM，用于与“浏览器”和“节点环境”(SSR)接口。对于某些场景，ReactDOM 的输出可用于测试。例如，下面是一个使用 ReactDOM 输出的“无状态组件的渲染结果是否符合预期”的测试(测试框架是 jest)。

```
it('should render stateless component', () => {
  const el = document.createElement('div');
  ReactDOM.render(<FunctionComponent name="A" />, el);
  expect(el.textContent).toBe('A');
});
```

有一个缺点，因为这个用例依赖于 DOM API 和浏览器环境(例如 document.createElement)。不言而喻，混合关于主机环境的信息会使测试用例更难构建，例如“React 的内部运行时机制”

## 2.如何测试并发环境？

如果在上面的用例中将 ReactDOM.render 更改为 ReactDOM.createRoot，那么这个用例将会失败。

```
*// before*
ReactDOM.render(<FunctionComponent name="A" />, el);
expect(el.textContent).toBe('A');

*// after*
ReactDOM.createRoot(el).render(<FunctionComponent name="A" />);
expect(el.textContent).toBe('A');
```

这是因为在新的架构下，很多以前的“同步更新”变成了“并发更新”，执行 render 时页面仍然在呈现。使上述用例起作用的最简单的方法是编辑

```
ReactDOM.createRoot(el).render(<FunctionComponent name="A" />);

setTimeout(() => {
  *//* synchronous
  expect(el.textContent).toBe('A');
})
```

你如何优雅地应对这种变化？

## React 的应对策略

React 团队的反应是我们要检查的下一件事。

让我们从解决第一个查询开始:渲染结果应该如何表示？

与与本机环境兼容的 ReactNative 相反，ReactDOM 对应于浏览器和节点环境。

那么，我们能否创建一个专门用于检查“内部运行时流”的渲染器呢？

是的，这就是答案。

React-Noop-Renderer 是该渲染器的名称。

简单来说，这个渲染器只会渲染 JS 对象。

## 实现渲染器

React 有一个内部包叫 Reconciler，里面引用了一些“操纵主机环境”的 API。

例如，下面的方法用于“将节点插入容器”。

```
function appendChildToContainer(child, container) {
 *//* Implement
}
```

对于浏览器环境(ReactDOM)，这是使用 appendChild 方法实现的。

```
function appendChildToContainer(child, container) {
  container.appendChild(child);
}
```

Reconciler 包通过 rollup 工具与上面的“用于浏览器环境的 API”打包在一起，就是 ReactDOM 包。在 React-Noop-Renderer 中，ReactDOM 中的 DOM 节点与以下数据结构对齐。

```
const instance = {
  id: instanceCounter++,
  type: type,
  children: [],
  parent: -1,
  props
};
```

请注意 children 字段，它用于保存子节点。因此，appendChildToContainer 方法可以在 React-Noop-Renderer 中实现，简单如下:

```
function appendChildToContainer(child, container) {
 const index = container.children.indexOf(child);
 if (index !== -1) {
  container.children.splice(index, 1);
 }
 container.children.push(child);
};
```

打包工具将 Reconciler 包与上面的“React-Noop 的 API”打包，这是 React-Noop-Renderer 包。基于 React-Noop-Renderer，您可以完全在正常的主机环境之外测试 Reconciler 的内部逻辑。接下来，我们来看第二个问题。

## 如何测试并发环境？

再复杂的“并发特性”，说到底也不过是“异步执行代码的各种策略”，最终执行它们的 API 无非就是 setTimeout、setInterval、Promise 等等。简而言之，您可以模拟这些异步 API 并控制它们的执行时间。例如，在上面的异步代码中，React 中的测试用例如下所示:

```
await act(() => {
  ReactDOM.createRoot(el).render(<FunctionComponent name="A" />);
})
expect(el.textContent).toBe('A');
```

act 方法，他的内部将执行 jest.runOnlyPendingTimers 方法，以便所有等待的计时器触发回调。例如，下面的代码:

```
setTimeout(() => {
  console.log('go');
}, 9999999)
```

jest.runOnlyPendingTimers 将在执行后立即打印“Execute”。这样，React 并发更新的速度就被人为控制了，对框架代码的入侵为零。此外，用于驱动并发更新的调度器模块本身也有一个测试版本。在这个版本中，开发人员可以手动控制调度程序的输入和输出。例如，我想测试组件卸载时 useEffect 回调的执行顺序。如下面的代码所示，其中 Parent 是挂载的“被测组件”。

```
function Parent() {
  useEffect(() => {
    return () => Scheduler.unstable_yieldValue('Unmount parent');
  });
  return <Child />;
}

function Child() {
  useEffect(() => {
    return () => Scheduler.unstable_yieldValue('Unmount child');
  });
  return 'Child';
}

await act(async () => {
  root.render(<Parent />);
});
```

useEffect 的逻辑是否如预期，可以通过 yieldValue 的插入顺序是否如预期来确定。

```
expect(Scheduler).toHaveYielded(['Unmount parent', 'Unmount child']);
```

## 在 React 中编写测试用例的策略是

*   可以用 ReactDOM 度量的用例，一般结合 ReactDOM 和 ReactTestUtils(浏览器环境的一个 helper 方法)来完成。
*   需要控制中间进程的用例，使用 Scheduler 的测试包，使用 Scheduler.unstable_yieldValue 记录进程信息。
*   如果你想在宿主环境之外单独测试 React 的内部进程，使用 React-Noop-Renderer。
*   要测试并发场景，您需要将上述工具与 jest-react 结合使用。

如果你想了解更多 React 中测试相关的技巧，可以看看 [RubyLouvre 的作品 anu](https://www.npmjs.com/package/anujs) 。

这是一个类似 React 的框架，但是可以运行 800 多个 React 用例。内部实现了 ReactTestUtils 的简化版本 React-Noop-Renderer。

***欢迎关注我上***[***Twitter***](https://twitter.com/yanghui0324)*[***LinkedIn***](https://www.linkedin.com/in/hui-yang-075076245/)***，以及***[***GitHub******！***](https://github.com/guchen-yh)*

*写作一直是我的激情所在，它给了我帮助和激励他人的快乐。如果您有任何问题，请随时联系我们！*

**更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW)*