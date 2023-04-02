# 对…的介绍🗺源地图

> 原文：<https://javascript.plainenglish.io/what-about-source-map-c7cf68b378dc?source=collection_archive---------11----------------------->

## 通过示例了解源地图。

![](img/31800e80a2b41d715125b268ef59f4a8.png)

*Mounting the Ox, slowly
I return homeward.
The voice of my flute intones
through the evening.
Measuring with hand-beats
the pulsating harmony,
I direct the endless rhythm.
Whoever hears this melody
will join me.
© Zen Ten Bulls*

嗨伙计们！

`[Source maps](https://developer.mozilla.org/en-US/docs/Tools/Debugger/How_to/Use_a_source_map)`无处不在！每次你打开一个网站，它就会加载成吨的缩小的`JavaScript`包，其中一些有`source maps`。它极大地简化了调试，所以经验法则是将它们添加到开发构建中。

> 使用[特殊注释](https://sourcemaps.info/spec.html#h.lmz475t4mvbx)将源映射嵌入到生成的源中。这些注释可能包含使用[数据 URI](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Data_URIs) 的整个源地图，或者可能引用外部 URL 或文件。
> 
> [node . js 中的源地图](https://nodejs.medium.com/source-maps-in-node-js-482872b56116)

在我们的例子中，使用了数据 URL。下面是[源图](https://www.html5rocks.com/en/tutorials/developertools/sourcemaps/)的一个例子:

```
{
    version : 3,
    file: "out.js",
    sourceRoot : "",
    sources: ["foo.js", "bar.js"],
    names: ["src", "maps", "are", "fun"],
    mappings: "AAgBC,SAAQ,CAAEA"
}
```

受益于源图的工具之一是:`[mock-import](https://github.com/coderaiser/mock-import)`。它有助于`mock`导入你正在使用的，所以你可以很容易地测试📼`[Supertape](https://github.com/coderaiser/supertape),`有史以来最伟大的跑步测试者😏！).

## 🗺源地图

当你需要一个`[sourcemap](https://github.com/coderaiser/putout#-sourcemap)`时，只需打电话就能轻松拥有🐊[输出](https://github.com/coderaiser/putout)用:

*   ✅ `sourceFileName`
*   ✅ `sourceMapName`

```
putout(source, {
    fix: false,
    sourceFileName: 'hello.js',
    sourceMapName: 'world.js',
    plugins: [
        'remove-unused-variables',
    ],
});
// returns
({
    code: '\n' +
    `    const hello = 'world';\n` +
    `    const hi = 'there';\n` +
    '    \n' +
    '    console.log(hello);\n' +
    '// {"version": 3, ...}',
    places: [{
        rule: 'remove-unused-variables',
        message: '"hi" is defined but never used',
        position: {line: 3, column: 10},
    }],
});
```

今天就到这里吧！有一张漂亮的地图🦉 🥳!

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*