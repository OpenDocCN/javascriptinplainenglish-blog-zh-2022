# 在 React 中渲染动态组件

> 原文：<https://javascript.plainenglish.io/rendering-dynamic-components-in-react-c859704492a?source=collection_archive---------12----------------------->

## 指南

## 有许多方法可以动态地呈现组件，让我们来看看一些方法。

![](img/08f2368041076eb85b3a1b950c887289.png)

[Credits](https://res.cloudinary.com/practicaldev/image/fetch/s--Vy_yXzCy--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/y2ur8p8rgkf778lwdtrv.jpg)

# 介绍

在我们的职业生涯中，有很多时候一个单一的因素是不够的。在本教程中，一个名为 useScreenSize 的钩子将根据屏幕大小返回三种状态:桌面、平板和移动。我们要为每个状态渲染一个不同的组件。

DesktopLayout.ts 当它返回桌面时，TabletLayout.ts 用于平板电脑，MobileLayout.ts 用于移动设备。

本文的所有代码都可以在[这里](https://codesandbox.io/s/old-darkness-1tpz6i?file=/src/App.js)找到。

# If / Else 模式

我们学到的第一个调节应用程序流量的方法是我们如何解决这个问题。通过使用 if/else 语句。这是一个简单的问题解决方案，但是在 React 中呈现动态组件时，不建议使用 If else 语句，因为它们会变得复杂和难以阅读。此外，if else 语句需要编写大量代码来呈现一个组件，这使得它很难维护。此外，if else 语句很难调试，因为有很多潜在的失败点。

```
 const WithIfs = ({ size }) => {
  if (size === "mobile") {
    return <MobileLayout />;
  }
  if (size === "tablet") {
    return <TabletLayout />;
  }
  return <DesktopLayout />;
};
```

# 开关模式

我们可以应用一个切换模式来稍微整理一下这种情况。这种策略有一些限制。开关不能直接用于你的渲染方法或函数的返回。相反，必须在我们的类中定义一个从我们的开关返回适当项的方法。在功能组件中，我们可以使用 reactions use memo 钩子来确保我们有正确的项目。

```
// Class based
class MyComponent {
 renderSwitch(param) {
  let Component;
  switch (param) {
    case "mobile":
      Component = MobileLayout;
      break;
    case "tablet":
      Component = TabletLayout;
      break;
    default:
      Component = DesktopLayout;
  }
  return <Component />;
 }

 render() {
  return (
    <div>
      <div>
          // stuff
      </div>
      {this.renderSwitch()} // will render desktop as we have no param
      <div>
          // stuff
      </div>
    </div>
  );
 }
}

// functional based
const MyComponent = ({ someProp }) => {
    const DivToRender = useMemo(() => {
       let Component;
      switch (param) {
        case "mobile":
          return MobileLayout;
        case "tablet":
          return TabletLayout;
        default:
          return DesktopLayout
      }
    }, [someProp])

    return ( 
        <div>
          <div>
          // removed for brevity
          </div>
          <DivToRender />
          <div>
             // removed for brevity
          </div>
       </div>
}
```

虽然这种模式可行，但我们遇到了与 if/else 块相同的问题，随着屏幕大小的增加，运行时复杂度仍然为 O(n ),找到正确项目所需的时间也增加了。Switch 语句没有针对性能进行优化。

Switch 语句不是为处理大量组件而设计的，因为它们使用线性搜索来查找正确的案例。这可能会导致大量不必要的计算时间，尤其是当您有很多组件时。此外，switch 语句不是为需要频繁更改的组件设计的，因为每次组件更改时都需要编辑代码。我们可以通过使用 useMemo 稍微减轻这一点。

# 对象映射模式

这就把我们带到了最后一个模式，我称之为对象映射模式。在这个模式中，我们将所有的组件存储在一个对象中。

```
const DynamicComponentMap = {
  DESKTOP: DesktopComponent,
  TABLET: TabletComponent,
  MOBILE: MobileComponent,
}

const MyResponsiveComponent = (props) => {
   const { screenSize } = useScreenSize();
   const Component = DynamicComponentMap[screenSize];
   return <Component {...props} />
}
```

这种方法的美妙之处在于，我们也不会受到简单的基于屏幕大小的按键的限制。假设我们有一个需要为多个用户呈现动态组件的仪表板。我们可以像下面这样做。

```
const Components = {
  DesktopAdmin,
  DesktopUser,
  DesktopSuperAdmin,
// ... more components here
}

const getUserComponents = userAuthLevel => {
   if (userAuthLevel === 'user') {
     return ['DesktopUser', 'PanelUser', 'OtherComponentUser']
   }
}

const getUserComponentsWithProps = userAuthLevel => {
   if (userAuthLevel === 'user') {
     return [{ componentName: 'DesktopUser', props: { some: 'prop'},]
   }
}

const DynamicDashboard = () => {
   const userComponents = getUserComponents('user');

   return (
      <div>
          {userComponents.map(componentName => {
              const Component = Components[componentName];
              return <Component />
           })
      </div>
  )
}

const DynamicDashboardWithDynamicProps = () => {
   const userComponents = getUserComponentsWithProps('user');

   return (
      <div>
          {userComponents.map(({ componentName, props }) => {
              const Component = Components[componentName];
              return <Component {...props}/>
           })
      </div>
  )
}
```

使用 JavaScript 对象代替 switch 语句或 if/else 进行动态呈现在几个方面具有优势。JavaScript 对象比 switch 语句更简洁，也更容易阅读和理解。JavaScript 对象也更加通用，使开发人员能够完成比 switch 语句更复杂的任务。最后，JavaScript 对象更容易维护和调试，因为它们很容易修改或替换。所有这些因素使得使用 JavaScript 对象代替 switch 语句进行动态呈现成为更好的选择。

## 让它更有性能

为了确保所有这些组件不会在构建时捆绑在一起，我们还可以使用 reactions Lazy system 惰性加载它们。React 惰性加载是一种提高 web 应用程序性能的好方法，它只在需要的时候加载组件。这有助于减少页面的初始加载时间，并带来更好的用户体验。此外，延迟加载可用于仅加载当前页面所需的组件，这将有助于减小应用程序的整体大小。最后，它可以帮助进行代码拆分，这有助于减少浏览器需要下载和解析的代码量，使应用程序更快、更高效。

# 结论

虽然我说基于对象的方法是最好的，但这些方法都可以工作，并且都取决于你们每个人的用例，我希望这篇文章给了你一些灵感/想法，帮助你解决这些问题，如果你有这些问题的话。

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

报名参加我们的 [**免费周报**](http://newsletter.plainenglish.io/) 。关注我们 [**推特**](https://twitter.com/inPlainEngHQ) ，[**LinkedIn**](https://www.linkedin.com/company/inplainenglish/)**，**[**YouTube**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)**，** [**不和谐**](https://discord.gg/GtDtUAvyhW) **。**

## 想用内容来扩展你的科技创业吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。

我们提供免费的专家建议和定制解决方案，帮助您建立对您的技术产品或服务的认知和采用。