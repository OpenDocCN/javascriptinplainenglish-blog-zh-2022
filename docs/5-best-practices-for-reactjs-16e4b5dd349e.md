# React 的 5 个最佳实践:简化 React 应用的构建过程

> 原文：<https://javascript.plainenglish.io/5-best-practices-for-reactjs-16e4b5dd349e?source=collection_archive---------6----------------------->

## 使用这些技巧来简化高性能 React 应用程序的构建过程。

![](img/b43f1480595803887716e20d756a6edc.png)

大家好，在本文中，我们将讨论 5 个最佳的 React 实践，它们将帮助您简化构建优秀的高性能应用程序。

# 使用片段

我们知道 React 一次只允许返回一个 JSX 元素，为了包装多个元素，我们使用了添加到 Dom 中的 div，这将需要一些计算，所以尝试使用 Fragment 而不是不必要的 div。

```
const withoutFragment = () => {
  return (
    <div>
      <h2>Without Fragment</h2>
      <p>Using div as external element</p>
    </div>
  );
};const withFragment = () => {
  return (
    <React.Fragment>
      <h2>With Fragment</h2>
      <p>Using React Fragment as external element</p>
    </React.Fragment>
  );
};
```

# 将大组件分解成小组件或可重用组件

如果组件太大，那么就将组件分解，将小组件组合成一个组件，并根据需要重用它们。

```
// Component (Before)
const ProfileCard = (props) => {
  return (
    <div className="card">
      <div className="avatar">
        <div className="icon">
          <span>{props.icon}</span>
        </div>
        <div className="name">
          <h2>{props.name}</h2>
        </div>
      </div>
      <div className="stats">
        <div className="followers">
          <span>{props.followers}</span>
          <p> Followers</p>
        </div>
        <div className="blogs">
          <span>{props.blogs}</span>
          <p> Articles</p>
        </div>
        <div className="revenue">
          <span>{props.revenue}</span>
          <p>MRR</p>
        </div>
      </div>
    </div>
  );
};// Small components with composition
const Avatar = ({ icon, name }) => {
  return (
    <div className="avatar">
      <div className="icon">
        <span>{icon}</span>
      </div>
      <div className="name">
        <h2>{name}</h2>
      </div>
    </div>
  );
};const Stats = ({ followers, blogs, revenue }) => {
  return (
    <div className="stats">
      <div className="followers">
        <span>{followers}</span>
        <p> Followers</p>
      </div>
      <div className="blogs">
        <span>{blogs}</span>
        <p> Articles</p>
      </div>
      <div className="revenue">
        <span>{revenue}</span>
        <p> MRR</p>
      </div>
    </div>
  );
};// Component with simplify JSX (After)
const ProfileCard = (props) => {
  return (
    <div className="card">
      <Avatar icon={props.icon} name={props.name} />
      <Stats
        followers={props.followers}
        blogs={props.blogs}
        revenue={props.revenue}
      />
    </div>
  );
};
```

# 使用类型检查

在应用程序中使用 propTypes 或 TypeScript 进行类型检查，以便尽早发现错误并防止 bug。

```
import PropTypes from 'prop-types';
const TypeChecking = ({ name }) => {
  return <h1>Hello, {name}</h1>;
};
TypeChecking.propTypes = {
  name: PropTypes.string.isRequired
};
```

# 使用功能组件

React haș引入了钩子，这对于在 ReactJs 中创建一个功能组件来说是很棒的，它让你可以毫不复杂地管理状态。

```
const Counter = () => {
  const [count, setCount] = React.useState(0);
  const handleClick = () => {
    setCount((prevCount) => prevCount + 1);
  };
  React.useEffect(() => {
    // It will be logged  when count value changes
    console.log('Count: ', count);
  }, [count]);
  return (
    <React.Fragment>
      <button onClick={handleClick}>Increment</button>
      <h2>{count}</h2>
    </React.Fragment>
  );
};
```

# 使用记忆

尝试使用 React memo 来避免不必要的重新渲染并提高应用程序性能。

```
const Child = React.memo(({ name }) => {
  console.log('Child rendering');
  return <p>{name}</p>;
});const Parent = () => {
  const [count, setCount] = React.useState(0);
  const handleClick = () => {
    setCount((prevCount) => prevCount + 1);
  };
  console.log('Parent rendering');
  return (
    <React.Fragment>
      <button onClick={handleClick}>Increment</button>
      <h2>{count}</h2>
      <Child name={'deuex solutions'} />
    </React.Fragment>
  );
};
```

如果您执行代码，那么您将看到子组件只被渲染一次。点击`increment`按钮，计数会增加，只有父组件会被重新渲染。

这个话题到此为止。感谢您的阅读。

# 与我联系

[LinkedIn](https://www.linkedin.com/in/sachin-chaurasiya) | [Twitter](https://twitter.com/sachindotcom)

*原发布于*[*https://blog . sachinchurasiya . dev*](https://blog.sachinchaurasiya.dev/5-best-practices-for-reactjs)*。*

*更多内容请看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。***