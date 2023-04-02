# 安排、行动和断言

> 原文：<https://javascript.plainenglish.io/arrange-act-and-assert-464219722a51?source=collection_archive---------3----------------------->

## 如何正确地组织你的测试(一个完整的例子)

![](img/092734c9f8ef22ed2c92eee4502b0411.png)

Photo by [Martin W. Kirst](https://unsplash.com/fr/@nitram509?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

当在编程中编写测试时，我们希望能够理解测试。不仅仅是为了我们自己，也是为了其他遇到我们代码的开发者。

编写适当组织的测试可以确保我们的代码被很好地记录，并且它应该是这样的，一个新的开发人员仅仅通过通读测试就能够理解我们的代码在做什么。

构建我们的测试的最有效的方法之一是使用**安排、动作和断言方法**。我喜欢这种技术，因为它简单并且允许我们一次只关注一个测试。

我以前写过，测试代码的最佳实践之一是避免在一次测试中有太多的断言。您可以点击[此链接](https://medium.com/javascript-in-plain-english/7-testing-best-practices-i-have-learned-as-a-developer-b8f469778443)阅读其余的最佳实践。

在这篇文章中，我将使用一个简单的例子来快速解释这种技术。

*注意:本例中选择的库是 react 测试库。*

## 我们将测试的示例组件

假设我们有一个按钮组件，我们想测试它的点击动作。

```
// The component
import Button from '...'

type MyButtonProps = {
  onClick: () => void,
  buttonText: string,
  testID: string,
}

const MyButton = ({ onClick, buttonText, testID }: MyButtonProps) => (
  <Button
    onClick={onClick}
    testID={testID}
    accessibilityRole='button'
  >
    {buttonText}
  </Button>
)
```

## 编写测试(一步一步)

为了开始编写测试，我们需要建立一个测试文件。这可能是类似于`MyButton.spec.tsx`或`MyButton.test.tsx`的东西。做完这个我们就可以开始测试了。

**(1)第一步是安排我们的考试。**

这意味着我们需要建立一个测试用例，并从用户的角度回答一些问题。我们可以问的第一个问题是，组件是用它的道具渲染的吗？

```
describe('MyButton component', () => {
  it('renders successfully with props', () => {
    // Arrange <--- We are here
    const props = {
      buttonText: 'My Button',
      testID: 'my-button-component'
    }
  })

  it('fires an on click action when clicked', () => {
    // Arrange <--- We are here
    const onClickMockFunction = jest.fn();
    const props = {
      buttonText: 'My Button',
      onClick: onClickMockFunction,
      testID: 'my-button-component'
    }
  })
})
```

在上面的代码片段中，我们已经安排了测试。也就是说，我们已经建立了我们的测试用例，现在我们可以继续与组件进行实际的交互。

**(2)第二步，按照我们安排好的测试用例行动。**

这意味着我们需要针对特定的行为。在本例中，我们将针对两种类型的行为；(1)它应该显示按钮文本 prop ,( 2)单击按钮时应该调用 click 函数。

```
describe('MyButton component', () => {
  it('renders successfully with props', () => {
    // Arrange
    const props = {
      buttonText: 'My Button',
      testID: 'my-button-component'
    }

    // Act <--- We are here
    const { getByText } = render(<MyButton {...props} />)
    fireEvent.click(screen.getByText(/my button/i))
  })

  it('fires an on click action when clicked', () => {
    // Arrange
    const onClickMockFunction = jest.fn();
    const props = {
      buttonText: 'My Button',
      onClick: onClickMockFunction,
      testID: 'my-button-component'
    }

    // Act <--- We are here
    const { getByText } = render(<MyButton {...props} />)
    fireEvent.click(screen.getByText(/my button/i))
  })
})
```

在上面的例子中，我们通过组件的文本内容来定位组件。我们也可以用其他方式来瞄准它:

```
const { getByTestID } = render(<MyButton {...props} />) // we would use 'my-button-component'
const { getByRole } = render(<MyButton {...props} />) // we would use 'button'

// For multiple buttons on the screen you can differentiate them like this:

screen.getByRole('button', { name: 'My Button 1' })
screen.getByRole('button', { name: 'My Button 2' })
```

**(3)第三步，也是最后一步，做断言。**

这意味着我们需要告诉我们的测试期望一个特定的结果。这将告诉我们测试是通过了还是失败了。我们使用`expect`关键字来做这件事。

```
describe('MyButton component', () => {
  it('renders successfully with props', () => {
    // Arrange
    const props = {
      buttonText: 'My Button',
      testID: 'my-button-component'
    }

    // Act
    const { getByText } = render(<MyButton {...props} />)

    // Assert <--- We are here
    expect(screen.getByText(/my button/i)).toBeDefined()
  })

  it('fires an on click action when clicked', () => {
    // Arrange
    const onClickMockFunction = jest.fn();
    const props = {
      buttonText: 'My Button',
      onClick: onClickMockFunction,
      testID: 'my-button-component'
    }

    // Act
    const { getByText } = render(<MyButton {...props} />)
    fireEvent.click(screen.getByText(/my button/i))

    // Assert <--- We are here
    expect(onClickMockFunction).toHaveBeenCalled()
  })
})
```

感谢阅读！

如果这是有帮助的，如果你给这篇文章一个👏在你的社交网络中分享，如果你还没有，关注一下会很好。

也请考虑通过我的[推荐](https://mazaher-muraj.medium.com/membership)链接订阅 Medium。Medium 是一个很好的学习平台，我用它来了解技术领域的最新动态，并学习其他开发人员的经验。

你的订阅将直接支持我和许多其他媒体作家。

[](https://mazaher-muraj.medium.com/membership) [## 通过我的推荐链接加入媒体

### 阅读 Mazaher Muraj(以及媒体上成千上万的其他作家)的每一个故事。您的会员费直接支持…

mazaher-muraj.medium.co](https://mazaher-muraj.medium.com/membership) 

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *

## *想扩大你的软件创业规模吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。*