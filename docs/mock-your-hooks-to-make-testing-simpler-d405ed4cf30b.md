# 模仿你的钩子来简化测试

> 原文：<https://javascript.plainenglish.io/mock-your-hooks-to-make-testing-simpler-d405ed4cf30b?source=collection_archive---------0----------------------->

## 用笑话来嘲讽会有一个奇怪的学习曲线。让我们看看如何嘲笑那些钩子。

![](img/6dbc992117bca6549ad9d928cd59cf69.png)

Photo by Steve Johnson: [https://www.pexels.com/photo/selective-focus-of-stainless-steel-hook-1256916/](https://www.pexels.com/photo/selective-focus-of-stainless-steel-hook-1256916/)

在本文中，我们将对**模仿我们的钩子**感兴趣，以使我们的 react 组件的**测试更容易**。

React 中单元测试的目标是能够测试特定文件**中的所有内容，而不受另一个模块**的任何干扰。

> 嘲讽允许我们通过忽略其他模块的逻辑并强制它们返回一个特定的值来保持其他模块的结果不变。

所以让我们开始吧！

# 做好准备

> 出于本文的考虑，我将假设您有一个用 Jest 和 React 测试库设置的 React 环境。如果没有，网上有很多教程可以帮助你快速设置！

在开始我们的教程之前，我们将准备一些文件。

首先，我们需要一个钩子来模仿:

```
// useNumber.js
const useNumber = () => {
    return 4;
}
export default useNumber;
```

这里我们想保持简单，只是一个简单的名为`useNumber`并返回数字 4 的“钩子”。我们不需要更多的复杂性！

然后我们需要一个使用这个钩子的 React 组件:

```
// App.js
import useNumber from './useNumber';

function App() {
  const number = useNumber();
  return (
    <div>
      {number}
    </div>
  );
}
```

这里再一次，非常简单的组件，我们不需要更多的东西！

最后，我们正在编写测试。正如我们在嘲讽钩子一样，我们的最终目标是我们的钩子不要返回 4:

```
// App.test.js
import {render} from '@testing-library/react';
import App from './App';

describe('App', () => {
    it('The hook should be mocked', () => {
        const {queryByText} = render(<App />);
        expect(queryByText('3')).not.toBeNull();
        expect(queryByText('4')).toBeNull();
    })
})
```

现在我们准备开始了！

# 方法 1:在顶层嘲讽

在这篇文章中，我们将以两种不同的方式嘲笑我们的钩子。 *(我会在文末说挑哪个。敬请期待！)*

第一种方法是**在测试的顶层模仿我们的钩子**。这样做将使这个文件中的所有测试都能够进行模拟。

```
***jest***.mock('./useNumber', () => {
    return () => 3;
});

describe('App', () => {
    it('The hook should be mocked', () => {
        const {queryByText} = render(<App />);
        expect(queryByText('3')).not.toBeNull();
        expect(queryByText('4')).toBeNull();
    })
})
```

我们使用`jest.mock`来模仿。作为第一个参数，它获取要模拟的文件的路径。

> 请记住，如果您的测试文件与要模拟的文件不在同一级别，那么路径将会不同。相对路径总是相对于测试文件，而不是被测试的组件。

`jest.mock`采用的第二个参数是新模块(模拟模块)的实现。它的结构总是这样:

```
() => <implementation>
```

第一个箭头函数称为`factory`，需要返回新的实现。执行以下操作无效:

```
***jest***.mock('./useNumber', {
    return () => 3;
});
```

现在回到我们的新实现，我们正在返回一个新函数(钩子是一个函数！)也就是返回 3。

开始了。我们的钩子现在被嘲笑了！试一试吧，你的考试会通过的！

# 方法 2:模拟每个测试

还有另一种方法来模仿你的钩子，那就是在**测试级别**。这种模拟将是每个测试都有的，并且允许你根据你的测试得到不同的返回值。

首先，我们需要对我们的`jest.mock`调用做一个小小的改变:

```
***jest***.mock('./useNumber');
```

如您所见，我**删除了第二个参数**，因为我们将在测试中直接模拟实现。

> 注意，删除默认值**不会将原始钩子设置为默认值**。取而代之的是，钩子会被自动嘲笑，不会返回任何值。我会在文章的**结尾做更多解释。**

现在，我们需要在测试中直接模拟钩子的返回值:

```
import useNumber from './useNumber'
...
it('The hook should be mocked', () => {
    useNumber.mockReturnValue(3);
    const {queryByText} = render(<App />);
    expect(queryByText('3')).not.toBeNull();
    expect(queryByText('4')).toBeNull();
})
```

开始了。现在，我们模拟了钩子的返回值，对于这个特定的测试，它将返回 3。

如果你喜欢，也可以用`mockImplementation`代替`mockReturnValue`:

```
useNumber.mockImplementation(() => 3);
```

> 请注意我是如何在我们的文件中导入`useNumber`的。这是因为我需要按照`jest.mock`所做的模拟来指定一个合适的返回值。

# 哪种方法比较好？

简单的答案是**没有。**

不足为奇的是，在软件编程中，**很少有一个问题的答案**。这通常取决于你需要什么。

## 第一种方法:静态的、全局的方法

第一种方法是**最好的，如果你只想把钩子固定在一个特定的值**上，然后在剩下的测试中忘掉它。它将保持静态，在你的文件的顶部，并将完美地完成这项工作。

## 第二种方法:更灵活，但有代价

如果你想用钩子的返回值来触发组件中不同的行为，第二种方法通常是最好的。对于 boolean 类型，您可能希望钩子根据测试返回 false 和 true，以确保您的组件适应它。

然而，这种方法有一个小缺点:你需要确定你为所有的测试定义了返回值 e。在你不这样做的情况下，jest 仍然会返回`jest.fn`，但是它可能会在你的结果中产生一些误报。所以要小心！

我希望这篇小文章能帮助你更好地理解这一点！嘲讽有时会有点棘手，因为如果你忘记了某处的箭头功能，Jest 可能会向你抛出一些未来错误。但是你从哪里弄来的，其实挺简单的！

我希望你喜欢这篇文章。如果你看到了，不要犹豫，跟我来或者留下一些掌声，因为它们很有帮助！

祝你度过愉快的一天(或一夜，取决于时区)！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*