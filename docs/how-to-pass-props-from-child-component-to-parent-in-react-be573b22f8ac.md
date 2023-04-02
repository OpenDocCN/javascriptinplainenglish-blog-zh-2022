# 如何在 React 中将道具从子组件传递到父组件

> 原文：<https://javascript.plainenglish.io/how-to-pass-props-from-child-component-to-parent-in-react-be573b22f8ac?source=collection_archive---------11----------------------->

![](img/f99870e80b6ded92f9ed3ae1473a32aa.png)

Photo by [Lautaro Andreani](https://unsplash.com/@lautaroandreani?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

是的，有可能！一个快速的谷歌搜索可能会给你混合的结果，但是从 2022 年开始，有一个干净、简单的方法可以使用回调来做到这一点。

有理由避免这样做，因为 React 旨在以一种数据从父节点流向子节点的方式进行设置，以避免多次重新渲染。一个更好的解决方案会涉及到上下文，但是如果你的需求很简单并且需要很快完成，这就是你实现它的方式。

# 步骤 1-设置一个状态和一个函数来获取父组件中的属性

设置一个从子组件获取道具的函数。在我的例子中，道具将是一个选定的“最喜爱的动物”。该选择将在子组件中进行，然后其值将传递给父组件。

设置状态:

```
const [favoriteAnimal, setFavoriteAnimal] = useState();
```

当然，如果您还没有导入 useState，请确保导入它。

我的函数看起来会像这样:

```
function passAnimal(data) {setFavoriteAnimal(data);}
```

# 2.在子组件中设置状态和调用函数

与上一步相同，我已经在子组件中添加了一个状态(只是给它一个默认值):

```
const [animal, setAnimal] = useState("cat");
```

我还需要调用我的函数

```
passAnimal(animal);
```

这里使用了我的动物变量，这样它就可以传递给我的父组件。如果您还没有添加 useState，请确保添加它，并将该函数作为一个 prop 传递，这样您的组件导出看起来就像这样:

```
export default function Child({ passAnimal }) {
...
```

为了这个例子，我还设置了一些无线电输入来选择动物。这里有一个例子:

```
<input type="radio" name="favoriteAnimal" value="cat" checked={animal === "cat"} defaultChecked={true} onChange={() => setAnimal("cat")} /><span>Cat{" "}<span role="img" aria-label="cat">🐈</span></span>
```

# 步骤 3 调用子组件时，将函数作为父组件中的传递

当您调用您的子组件时，请确保将您的函数作为道具传递。这将看起来像这样:

```
<Child passAnimal={passAnimal} />
```

就是这样！您应该在父组件的子组件中选择您的道具。

此处 Codesandbox 示例:[https://code sandbox . io/s/passing-props-from-child-to-parent-component-sxr3b 7？file=/src/components/App.js](https://codesandbox.io/s/passing-props-from-child-to-parent-component-sxr3b7?file=/src/components/App.js)

希望这对你有帮助。编码快乐！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) **