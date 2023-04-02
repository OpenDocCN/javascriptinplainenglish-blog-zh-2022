# 面向初学者的 Array.entries()介绍

> 原文：<https://javascript.plainenglish.io/inception-of-array-entries-840a3b725b1d?source=collection_archive---------17----------------------->

## 即使在需要使用`index`时，也要摆脱`for`循环。

![](img/94a9706f977cc356b6b61a1b6b16f62e.png)

*Along the riverbank under the trees,
I discover footprints.
Even under the fragrant grass,
I see his prints.
Deep in remote mountains, they are found.
These traces can no more be hidden
than one’s nose, looking heavenward.
© Zen Ten Bulls*

嗨伙计们！

今天我们来谈谈`[Array.entries](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/entries)()`，即使当你需要使用`index`时，它们也会帮助你摆脱`for`循环。在过去美好的日子里，我们用:

```
for (let i = 0; i < elements.length; i++) {
    const element = elements[i];
    console.log(i, element);
}
```

但是现在我们大部分时间都在使用`for-of`，因为它更简单，而且只做需要做的事情:

```
for (const element of elements) {
    console.log(i, element); // <-- we have no i 🍄
}
```

但是打住，有什么用`i`变量？我们应该从哪里得到它？
不用担心😄，`array.entries()`来救援了！

```
for (const [i, element] of elements.entries()) {
    console.log(i, element);
}
```

# `convert-for-to-for-of`

当然，这样的转变早已在等着你了🐊输出插件`[convert-for-to-for-of](https://github.com/coderaiser/putout/tree/v24.4.0/packages/plugin-convert-for-to-for-of#putout-plugin-convert-for-to-for-of-)`🎈。

# `remove-useless-array-entries`

但是，如果您使用`array.entries()`和`index`一段时间，然后停止使用 index，并且您的代码看起来像这样，该怎么办呢？

```
for (const [, element] of elements.entries()) {
    console.log(element);
}
```

不要担心！🐊输出插件`[remove-useless-array-entries](https://github.com/coderaiser/putout/tree/v24.4.0/packages/plugin-remove-useless-array-entries#putoutplugin-remove-useless-array-entries-)`将代码转换成通常的`for-of`:

```
for (const element of elements) {
    console.log(element);
}
```

伙计们玩得开心，总是使用`for-of`(除了需要大量速度☝️的热代码！)🦉。

*更多内容看* [***说白了就是***](http://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。*