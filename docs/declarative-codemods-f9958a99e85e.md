# 声明性代码模块🐊输出

> 原文：<https://javascript.plainenglish.io/declarative-codemods-f9958a99e85e?source=collection_archive---------11----------------------->

![](img/569bf780260c3a19a44c6cb8b390f840.png)

嗨伙计们！

![](img/4930bd68c1bbc2932c665713fda97493.png)

本文基于惊人的[“编写代码重写您的代码”](https://www.toptal.com/javascript/write-code-to-rewrite-your-code)文章。它告诉我们关于“ **jscodeshift** ”，这个工具有多好，以及如何用它编写 **codemods** 。

“jscodeshift”很棒，它在让 **codemods** 流行起来方面做得很好，但现在是新人登场的时候了—”🐊 [**输出**](https://github.com/coderaiser/putout) 😏。

看看吧！

# 练习 1:删除对控制台的呼叫

![](img/b0d56494278c49872f0456e8ad575aac.png)

假设我们有一个包含大量日志的代码:

```
**export** **const** sum = (a, b) => {
  console.log('calling sum with', arguments);
  **return** a + b;
};

**export** **const** multiply = (a, b) => {
  console.warn('calling multiply with',
    arguments);
  **return** a * b;
};

**export** **const** divide = (a, b) => {
  console.error(`calling divide with ${ arguments }`);
  **return** a / b;
};

**export** **const** average = (a, b) => {
  console.log('calling average with ' + arguments);
  **return** divide(sum(a, b), 2);
};
```

我们想删除所有的`console.log`调用表达式，并使用 jscodeshift 来实现这个目的:

```
**export** **default** (fileInfo, api) => {
  **const** j = api.jscodeshift;

  **const** root = j(fileInfo.source)

  **const** callExpressions = root.find(j.CallExpression, {
      callee: {
        type: 'MemberExpression',
        object: { type: 'Identifier', name: 'console' },
      },
    }
  );

  callExpressions.remove();

  **return** root.toSource();
};
```

好了，现在🐊 [**输出**](https://github.com/coderaiser/putout) :

```
**export const** replace = () => ({
    'console.__a(__args)': '',
});
```

这就是 [**Replacer**](https://github.com/coderaiser/putout/tree/master/packages/engine-runner#replacer) ，declarative 的写法 codemods。它有以下模板变量🦎**输出脚本**:

*   `__a` —是证明`property`在 [**成员表达式**](https://github.com/coderaiser/putout/blob/master/docs/the-book-of-ast.md#memberexpression) 中的位置的任何正确代码；
*   `__args` —任何类型的任何数量的自变量；

它所做的是将左侧的**表达式**或**语句**转换为右侧的 **AST** 并转换为右侧的 **AST** 。在当前情况下-删除节点。

> 🦎 [**输出脚本**](https://github.com/coderaiser/putout/blob/master/docs/putout-script.md) —兼容 JavaScript 的语言，为 AST-template 中的`[Identifiers](https://github.com/coderaiser/putout/blob/master/docs/the-book-of-ast.md#identifier)`增加了额外的含义。

和结果:

```
**export const** sum = (a, b) => {
  return a + b;
};

**export const** multiply = (a, b) => {
  return a * b;
};**export const** divide = (a, b) => {
  return a / b;
};**export const** average = (a, b) => {
  return divide(sum(a, b), 2);
};
```

在以下位置签出🐊 [**输出编辑器**](https://putout.cloudcmd.io/#/gist/3c6af7f297a9e3712cfdde46c93ca648/00386b52a3476079a512756172ee585cf0a4c0f5) 和输入[@输出/插件-移除-控制台](https://github.com/coderaiser/putout/tree/master/packages/plugin-remove-console#readme)。

# 练习 2:替换导入的方法调用

![](img/aa5361019330a3e303f906dacad6ee64.png)

现在让我们观察调用`g.circleArea()`的代码:

```
**import** g from 'geometry';
**import** otherModule from 'otherModule';**const** radius = 20;
**const** area = **g**.**circleArea**(radius);console.log(area === Math.pow(g.getPi(), 2) * radius);
console.log(area === otherModule.circleArea(radius));
```

我们想把`circleArea`改成`getCircleArea`。以下是 **jscodeshift** 可以给出的建议:

```
**export** **default** (fileInfo, api) => {
  **const** j = api.jscodeshift;
  **const** root = j(fileInfo.source);

  *// find declaration for "geometry" import*
  **const** importDeclaration = root.find(j.ImportDeclaration, {
    source: {
      type: 'Literal',
      value: 'geometry',
    },
  });

  *// get the local name for the imported module*
  **const** localName =
    *// find the Identifiers*
    importDeclaration.find(j.Identifier)
    *// get the first NodePath from the Collection*
    .get(0)
    *// get the Node in the NodePath and grab its "name"*
    .node.name;

  **return** root.find(j.MemberExpression, {
      object: {
        name: localName,
      },
      property: {
        name: 'circleArea',
      },
    })

    .replaceWith(nodePath => {
      *// get the underlying Node*
      **const** { node } = nodePath;
      *// change to our new prop*
      node.property.name = 'getCircleArea';
      *// replaceWith should return a Node, not a NodePath*
      **return** node;
    })

    .toSource();
};
```

这是🐊**输出**版本:

```
**export const** replace = () => ({
    '__a.circleArea(__args)': '__a.getCircleArea(__args)',
});
```

如果我们需要更多与变量名`g`相关的检查:

```
**export const** match = () => ({
    '__a.circleArea(__args)': ({__a}, path) => {
        if (__a.name !== 'g')
            return false;

        return true;
    }
});**export const** replace = () => ({
    '__a.circleArea(__args)': '__a.getCircleArea(__args)',
});
```

`match`条件在`replace`之前起作用，所以我们有转换的前提条件。

以及检查`import`绑定的`1 x 1` varian，然后[比较](https://github.com/coderaiser/putout/tree/master/packages/compare)节点。

```
**export const** match = () => ({
    '__a.circleArea(__args)': ({__a}, path) => {
        const binding = path.scope.bindings[__a.name];
        return compare(binding.path.parentPath, 'import __a from "geometry"');
    }
});**export const** replace = () => ({
    '__a.circleArea(__args)': '__a.getCircleArea(__args)',
});
```

请查看🐊 [**输出编辑**](https://putout.cloudcmd.io/#/gist/3c6af7f297a9e3712cfdde46c93ca648/afe502ed2a184f781d44006450ce8198cf4dcf48) 。

结果如下:

```
**import** g from 'geometry';
**import** otherModule from 'otherModule';**const** radius = 20;
**const** area = **g**.**getCircleArea**(radius);console.log(area === Math.pow(g.getPi(), 2) * radius);
console.log(area === otherModule.circleArea(radius));
```

# 练习 3:更改方法签名

![](img/d3d64497b7313dcd470867304eddf37a.png)

而不是`car.factory('white', 'Kia', 'Sorento', 2010, 50000, null, true);`

我们想看看

```
**const** suv = car.factory({
  color: 'white',
  make: 'Kia',
  model: 'Sorento',
  year: 2010,
  miles: 50000,
  bedliner: null,
  alarm: true,
});
```

以下是 jscodeshift 可以给出的建议:

```
**export** **default** (fileInfo, api) => {
  **const** j = api.jscodeshift;
  **const** root = j(fileInfo.source);

  *// find declaration for "car" import*
  **const** importDeclaration = root.find(j.ImportDeclaration, {
    source: {
      type: 'Literal',
      value: 'car',
    },
  });

  *// get the local name for the imported module*
  **const** localName =
    importDeclaration.find(j.Identifier)
    .get(0)
    .node.name;

  *// current order of arguments*
  **const** argKeys = [
    'color',
    'make',
    'model',
    'year',
    'miles',
    'bedliner',
    'alarm',
  ];

  *// find where `.factory` is being called*
  **return** root.find(j.CallExpression, {
      callee: {
        type: 'MemberExpression',
        object: {
          name: localName,
        },
        property: {
          name: 'factory',
        },
      }
    })
    .replaceWith(nodePath => {
      **const** { node } = nodePath;

      *// use a builder to create the ObjectExpression*
      **const** argumentsAsObject = j.objectExpression(

        *// map the arguments to an Array of Property Nodes*
        node.arguments.map((arg, i) =>
          j.property(
            'init',
            j.identifier(argKeys[i]),
            j.literal(arg.value)
          )
        )
      );

      *// replace the arguments with our new ObjectExpression*
      node.arguments = [argumentsAsObject];

      **return** node;
    })

    *// specify print options for recast*
    .toSource({ quote: 'single', trailingComma: true });
};
```

这是一个简短的声明🐊**输出**变量:

```
**export const** replace = () => ({
    'car.factory(__a, __b, __c, __d, __e, __f, __g)': `car.factory({
        color: __a,
        make: __b,
        model: __c,
        year: __d,
        miles: __e,
        badliner: __f,
        alarm: __g,
     })`
});
```

在以下位置签出🐊 [**输出编辑**](https://putout.cloudcmd.io/#/gist/f9161353c8bbcbbf98e1851c4d212190/20bd5886e2234a2bb680b667ab68e8e599d35735) 。

# **鳍**

![](img/835f7ea91ecad958886c43b90b1fbaae.png)

正如您看到的🐊在声明性代码模块的支持下，输出为你提供了更好的体验。它还帮助您测试您的 codemods 并在 ESLint 环境中运行它们。

☝️follow me on medium/@[code raiser](https://medium.com/u/47c05fa2893e?source=post_page-----1782c6625d77--------------------------------)，了解如何提高您的编码技能😏。

☝️在 GitHub 上增加了明星⭐️，这很激励人！

如果你喜欢我正在做的事情，☝️支持我。

☝️And:记住，我会一直在这里解决你对我提出的代码的任何问题😋。

感谢您的阅读，祝您有美好的一天😸！

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***