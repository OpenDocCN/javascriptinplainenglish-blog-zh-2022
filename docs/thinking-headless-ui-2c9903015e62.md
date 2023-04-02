# 思考无头用户界面

> 原文：<https://javascript.plainenglish.io/thinking-headless-ui-2c9903015e62?source=collection_archive---------7----------------------->

![](img/f201e87b73be03582ba80044953cb9b9.png)

Image by [Tania Dimas](https://pixabay.com/users/taniadimas-1503346/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=993331) from [Pixabay](https://pixabay.com//?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=993331)

> 没有接口的组件…

## 无头哲学

Web 组件由两样东西组成，接口和驱动接口的逻辑。

将逻辑与接口分离是 headless 的核心理念。

它允许我们构建高度灵活、适应性强的 web 组件，这些组件可以跨 UI 库工作。

## 示例—一个独立的切换按钮

我们将让*使用*的 React 钩子来构建切换按钮。

为了构建按钮，我们需要一个**状态**来指示按钮是否被按下，以及一个事件处理程序**在点击时切换**状态。

> 类型定义

```
type ButtonPropsGetter = () => {
  onClick: (e: MouseEvent<HTMLButtonElement>) => void;
  "aria-pressed": "true" | "false";
};

type StateGetter = () => boolean;

type ToggleButtonGetters = {
  getButtonProps: ButtonPropsGetter;
  getState: StateGetter;
}; 
```

> 使用按钮挂钩

```
const useToggleButton = (): ToggleButtonGetters => {
  const [status, setStatus] = useState(false);

  const onClick = () => {
    setStatus((prev) => !prev);
  };

  const getButtonProps: ButtonPropsGetter = () => {
    return { onClick, "aria-pressed": status ? "true" : "false" };
  };

  const getState: StateGetter = () => status;

  return { getButtonProps, getState };
};
```

> 就是这样！我们可以很容易地使用它，无论是本机按钮还是任何其他 react 库

> 消费

```
import useToggleButton from "./useToggleButton";

const App: FC = () => {
  const { getButtonProps, getState } = useToggleButton();
  const status = getState();

  return (
    <div>
      <h1>Hello World!</h1>
      {/* We can replace this button with any button */}
      <button {...getButtonProps()}>{status ? "ON" : "OFF"}</button>
    </div>
  );
}
```

我们可以很容易地修改钩子来接受一个初始值，而不需要接触呈现部分，或者我们可以很容易地修改按钮，而不需要接触钩子部分。

## 流行的无头库

*   [转栈表](https://tanstack.com/table/v8)
*   [React Dropzone](https://react-dropzone.js.org/)
*   [降档](https://www.downshift-js.com/)

*谢谢。*

*更多内容看* [***说白了就是***](https://plainenglish.io/) *。*

*报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) ***。****

****有兴趣缩放你的软件启动*** *？检查出* [***电路***](https://circuit.ooo?utm=publication-post-cta) *。**