# 如何解决 Next.js 中的补水错误

> 原文：<https://javascript.plainenglish.io/how-to-solve-hydration-error-in-next-js-a50ec54bfc02?source=collection_archive---------0----------------------->

![](img/d6133a6e239b6656ad735c4b1cff3114.png)

今天我们来谈谈`Next.js`中经常出现的`hydration` 错误。我们大多数用过`Next.js`的人一定熟悉下面这个错误:

```
**Error**: Hydration failed because the initial UI does not match what was rendered on the server.
```

错误原因已经在错误消息中明确说明:**`**hydration**`**因水合后 UI 与服务器渲染的 UI**不一致而失败。尽管错误消息说水合失败，但是，它仍然显示可以认为渲染成功的正确 UI。**

## **让我们来谈一个商业案例**

**我们在本地存储一些不重要或不同步的数据，并在客户端获取这些本地存储的数据。比如我们在`localStorage`中存储了一些配置，页面会根据配置进行渲染。
以`sidebar`为例:**

```
export default function R() {
    const [expand, setExpand] = React.useState(() => localStorage.getItem(EXPAND_STORAGE_KEY) === '1');
    return (
        <div>
            <NavSidebar expand={expand} onExpand={setExpand} />
        </div>
    );
}
```

**我们有一个侧边栏，用户可以展开或折叠，我们经常在本地保存它的状态，以方便用户体验。**

**由于 Next.js 既有客户端渲染(`CSR`)又有服务器渲染(`SSR`)，代码将在客户端正确运行，但会导致服务器渲染(`SSR`)出错，因为服务器端缺少`localStorage` API。所以我们修改了代码:**

```
export default function R() {
    const [expand, setExpand] = React.useState(() =>
        typeof window === 'undefined' ? false : localStorage.getItem(EXPAND_STORAGE_KEY) === '1'
    );
    return (
        <div>
            <NavSidebar expand={expand} onExpand={setExpand} />
        </div>
    );
}
```

**我们通过`window`关键字检查是服务器还是浏览器环境，然后根据它运行不同的代码，那么我们开头说的错误就消失了。**

**上面的代码逻辑上看起来不错，但是在浏览器中运行就会出现上面的`hydration`错误。**

## **React 做检查而不是 Next.js**

**事实上，错误是由检查`React`中的`react-dom`而不是`Next.js.`引起的，我们可以简单地查看`react-dom`中的相关源代码:**

```
if (!tryHydrate(fiber, nextInstance)) {
    if (shouldClientRenderOnMismatch(fiber)) {
        warnNonhydratedInstance(hydrationParentFiber, fiber);
        throwOnHydrationMismatch();
    }
}
function throwOnHydrationMismatch(fiber) {
    throw new Error('Hydration failed because the initial UI does not match what was ' + 'rendered on the server.');
}
function shouldClientRenderOnMismatch(fiber) {
    return (fiber.mode & ConcurrentMode) !== NoMode && (fiber.flags & DidCapture) === NoFlags;
}
```

**`react-dom`中的代码将使用`tryHydrate`尝试水合物操作，如果失败，将检查模式和标志并抛出`hydration`错误。**

****这个错误怎么解决？有 3 个解决方案适合你。****

## **解决方案 1**

**`useEffect/componentDidMount`**

**要解决以上问题，官方推荐使用`useEffect`:**

```
const [expand, setExpand] = React.useState(true);

// to avoid ssr error
useEffect(() => {
    setExpand(localStorage.getItem(EXPAND_STORAGE_KEY) === '1');
}, []);
```

**不会抛出错误，因为效果不会在服务器上执行。当然也可以使用类组件，然后在`componentDidMount`中获取`localStorage`。然而，使用这种解决方案时会出现一些问题。比如有一个`sideBar`展开和折叠的动画，用户在进入页面时会看到一个额外的动画，会很奇怪。解决方案是不默认呈现`sidebar`。😂因此，`SSR`的效果并没有想象中的那么好，这真的要看实际业务了。**

## **解决方案 2**

**`react-no-ssr`**

**另一种解决方案是使用一些开源库，比如`react-no-ssr`。实际上，`react-no-ssr` 也是用`solution 1`实现的。你可以看看源代码:**

```
import React from 'react';

const DefaultOnSSR = () => <span></span>;

class NoSSR extends React.Component {
    constructor(...args) {
        super(...args);
        this.state = {
            canRender: false
        };
    }

    componentDidMount() {
        this.setState({ canRender: true });
    }

    render() {
        const { children, onSSR = <DefaultOnSSR /> } = this.props;
        const { canRender } = this.state;

        return canRender ? children : onSSR;
    }
}

export default NoSSR;
```

**可以看到`NoSSR`只会在`componentDidMount`中设置`canRender`，那么就会以正确的方式渲染。**

## **解决方案 3**

**`Turn Off SSR`**

**我们也可以通过关闭组件的`SSR`来解决问题。其实上面的`react-no-ssr`就是其中之一，但是`Next.js`还提供了一个内置的解决方案:**动态加载组件并关闭** `**SSR**`，以上面的`sidebar`为例:**

```
import dynamic from 'next/dynamic';

const DynamicSidebarWithNoSSR = dynamic(() => import('../components/Sidebar'), {
    ssr: false
});

export default function R() {
    return (
        <div>
            <DynamicSidebarWithNoSSR />
        </div>
    );
}
```

**我们只需要提取组件，然后使用`dynamic`加载组件并传入`SSR`参数作为`false`来关闭组件的服务器渲染。**

**当然，为了方便我们可以做一些工作:**

```
import dynamic from 'next/dynamic';
import React from 'react';

const NoSSR = props => <React.Fragment>{props.children}</React.Fragment>;

export default dynamic(() => Promise.resolve(NoSSR), {
    ssr: false
});
```

**然后我们只需要直接调用`NoSSR`来包装子组件:**

```
import dynamic from 'next/dynamic';
import Sidebar from '../components/Sidebar';

export default function R() {
    return (
        <div>
            <NoSSR>
                <Sidebar />
            </NoSSR>
        </div>
    );
}
```

## **结论**

**`CSR`仅限于在浏览器中运行，而`SSR`需要能够在浏览器和服务器中运行，这遇到了一些在纯`CSR`应用中没有出现的问题和挑战。在用户体验方面，`SSR`确实会给我们的应用带来很大的提升。**

**感谢阅读。期待期待您的关注和阅读更多高质量的文章。**

**[](https://levelup.gitconnected.com/the-story-of-clip-path-and-endangered-animals-in-css-8af987927fc6) [## CSS 中剪辑路径和濒危动物的故事

### 使用 CSS 剪辑路径创建奇妙的动画

levelup.gitconnected.com](https://levelup.gitconnected.com/the-story-of-clip-path-and-endangered-animals-in-css-8af987927fc6) [](/which-loop-traversal-is-the-fastest-in-javascript-c196311337d6) [## JavaScript 中哪个循环遍历最快？

### JavaScript 数组遍历方法的比较

javascript.plainenglish.io](/which-loop-traversal-is-the-fastest-in-javascript-c196311337d6) [](/identify-javascript-data-types-two-methods-are-enough-882e2c238e6b) [## 识别 JavaScript 数据类型:两种方法就足够了

### 引入一个实用方法来识别所有数据类型

javascript.plainenglish.io](/identify-javascript-data-types-two-methods-are-enough-882e2c238e6b) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***