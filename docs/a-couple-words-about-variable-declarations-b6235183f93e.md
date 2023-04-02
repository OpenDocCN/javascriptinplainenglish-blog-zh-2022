# 关于变量声明的几句话

> 原文：<https://javascript.plainenglish.io/a-couple-words-about-variable-declarations-b6235183f93e?source=collection_archive---------22----------------------->

## 关于 Putout 以最简单的方式声明和处理变量的能力的介绍性指南！

![](img/f6fede1cd002aaa2a8644d9078faf5c2.png)

*I seize him with a terrific struggle.
His great will and power
are inexhaustible.
He charges to the high plateau
far above the cloud-mists,
Or in an impenetrable ravine, he stands.
© Zen Ten Bulls*

嗨伙计们！

今天，我想告诉你一个有用的功能，这是大幅改善。

# `[operator.getBindingPath](https://github.com/coderaiser/putout/tree/v23.3.0/packages/operate#getbindingpathpath-name-string--node)`和变量声明

让我们从代码示例开始:

```
const x  = {
   y: 'hello',
};typeof hello === 'string';
typeof x.y === 'number';
```

如何确定`hello`变量是否声明？让我们试着解决它。

当你有一个像这样的`path`时，你可以在`[Replacer](https://github.com/coderaiser/putout/tree/v24.5.0/packages/engine-runner#replacer)`中使用`match`:

```
const {operator} = require('putout');
const {getBindingPath} = operator;module.exports.match = () => ({
    'typeof __a === "__b"': ({__a}, path) => {
        // when __a declared proceed to replace
        return getBindingPath(path, __a))
    }
});
```

当你想知道节点`__a`是否被声明时，你可以使用`getBindingPath`，它会解决这个问题:

```
getBindingPath(path, 'hello');
// returns
null;getBindingPath(path, 'x');
// returns
Path;
```

但是如果你不知道你将要收到的`node`是什么类型，但是你明确地知道你需要这个`node`的名字来继续呢？只需传递`node`和`getBindingPath`将为您解析名称:)！

```
getBindingPath(path, node); // node can be Identifier or MemberExpression
// parse the name first, and then find it's declaration
Path;
```

# `convert-typeof-to-is-type`的新能力。

现在`[convert-typeof-to-is-type](https://github.com/coderaiser/putout/tree/v24.5.0/packages/plugin-convert-typeof-to-is-type#readme)`支撑`MemberExpressions`良好；

```
const hello = {
    world: '',
};// before:
typeof hello.world === 'string'// after:
isString(hello.world);
```

在`[declare-undefined-variables](https://github.com/coderaiser/putout/tree/v23.3.0/packages/plugin-declare-undefined-variables#readme)`的帮助下，您将获得:

```
// a new declaration
const isString = (a) => typeof a === 'string';const hello = {
    world: '',
};isString(hello.world);
```

两者并用才能获得最大收益！🎈默认情况下，它们是启用的😏。

# `Includer`的自动修复

当你使用`[Includer](https://github.com/coderaiser/putout/tree/v24.5.0/packages/engine-runner#includer)`时，由于某种原因，忘记了它需要一个返回数组的函数`[putout/includer](https://github.com/coderaiser/putout/tree/v23.3.0/packages/plugin-putout#includer)`会帮你搞定！

还有这样的代码:

```
module.exports.include = [
    'const __a = __b',
];
```

甚至这样:

```
module.exports.include = 'const __a = __b';
```

将被转换为唯一正确的选项:

```
module.exports.include = () => [
    'const __a = __b',
];
```

☝️让事情运转起来启用`.putout.json`中的`putout`规则:

```
{
    "rules": {
        "putout": "on"
    }
}
```

总是使用最简单的插件类型来满足你的需求🍬。

今天就到这里吧！

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。***