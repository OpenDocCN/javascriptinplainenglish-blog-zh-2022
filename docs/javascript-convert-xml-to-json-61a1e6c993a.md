# 如何在 JavaScript 中将 XML 转换为 JSON

> 原文：<https://javascript.plainenglish.io/javascript-convert-xml-to-json-61a1e6c993a?source=collection_archive---------10----------------------->

## 了解如何在 JavaScript 中轻松地将 XML 数据转换为 JSON 数据。

![](img/3798c55e8b89931738605fc364577b61.png)

我们可以使用 NPM 的`xml-js`库很容易地将 XML 转换成 JavaScript 中的 JSON。

```
import { xml2json } from 'xml-js';const json = xmltojson(xml);
```

可扩展标记语言(XML)是一种类似于 HTML 的标记语言，旨在存储和传输数据。与 HTML 不同，XML 没有任何预定义的标签。相反，我们根据自己的需求定义自己的标签。

JavaScript 对象表示法(JSON)是一种基于 JavaScript 对象语法用于存储和传输数据的文本格式，通常用于构建 RESTful APIs。

我们可以通过`xml-js`用 JavaScript 将 XML 数据转换成 JSON 数据:

```
import { xml2json } from 'xml-js';const xml = `<name>Garage</name>
<cars>
    <color>red</color>
    <maxSpeed>120</maxSpeed>
    <age>2</age>
</cars>
<cars>
    <color>blue</color>
    <maxSpeed>100</maxSpeed>
    <age>3</age>
</cars>
<cars>
    <color>green</color>
    <maxSpeed>130</maxSpeed>
    <age>2</age>
</cars>`;const json = xmltojson(xml, );console.log(json);
```

该代码将具有以下 JSON 输出:

```
{"declaration":{"attributes":{"version":"1.0","encoding":"UTF-8"}},"elements":[{"type":"element","name":"languages","elements":[{"type":"element","name":"language","elements":[{"type":"text","text":"\n      English\n   "}]},{"type":"element","name":"language","elements":[{"type":"text","text":"\n      French\n   "}]},{"type":"element","name":"language","elements":[{"type":"text","text":"\n      Spanish\n   "}]}]}]}
```

# 安装 xml-js

在使用`xml-js`之前，我们需要在我们的项目中安装它。我们可以通过 NPM 命令行界面来实现这一点。

```
npm i xml-js
```

或使用纱线 CLI:

```
yarn add xml-js
```

安装后，我们将能够将其导入一个 JavaScript 模块，如下所示:

```
import { xml2json } from 'xml-js';
```

我们使用导入破坏直接从库中访问`xml2json()`方法。

对于 CommonJS 模块，我们将像这样导入它:

```
const { xml2json } = require('xml-js');
```

# `xml2json()`功能

`xml2json()`功能有两个参数。第一个是要转换为 JSON 的 XML 字符串，第二个是可选对象。

```
const json = xml2json(xml, { spaces: 2, compact: true });
```

# 自定义 XML 到 JSON 的转换

我们使用这个对象来指定定制转换过程的各种选项。

在我们的示例中，我们不传递对象，所以使用默认选项。我们可以传递一个带有`spaces`选项的对象来正确格式化和缩进生成的 JSON。

```
import { xml2json } from 'xml-js';const xml = `<?xml version="1.0" encoding="UTF-8"?>
<languages>
   <language>
      English
   </language>
   <language>
      French
   </language>
   <language>
      Spanish
   </language>
</languages>`;// 👇 Set "spaces" option
const json = xml2json(xml, { spaces: 2 });console.log(json);
```

以下是新的输出:

```
{
  "declaration": {
    "attributes": {
      "version": "1.0",
      "encoding": "UTF-8"
    }
  },
  "elements": [
    {
      "type": "element",
      "name": "languages",
      "elements": [
        {
          "type": "element",
          "name": "language",
          "elements": [
            {
              "type": "text",
              "text": "\n      English\n   "
            }
          ]
        },
        {
          "type": "element",
          "name": "language",
          "elements": [
            {
              "type": "text",
              "text": "\n      French\n   "
            }
          ]
        },
        {
          "type": "element",
          "name": "language",
          "elements": [
            {
              "type": "text",
              "text": "\n      Spanish\n   "
            }
          ]
        }
      ]
    }
  ]
}
```

`compact`属性，用于确定生成的 JSON 应该是详细的还是紧凑的。默认为`false`。

```
import { xml2json } from 'xml-js';const xml = `<?xml version="1.0" encoding="UTF-8"?>
<languages>
   <language>
      English
   </language>
   <language>
      French
   </language>
   <language>
      Spanish
   </language>
</languages>`;// 👇 Set "compact" option
const json = xml2json(xml, { spaces: 2, compact: true });console.log(json);
```

现在，生成的 JSON 的大小将比以前小得多:

```
{
  "_declaration": {
    "_attributes": {
      "version": "1.0",
      "encoding": "UTF-8"
    }
  },
  "languages": {
    "language": [
      {
        "_text": "\n      English\n   "
      },
      {
        "_text": "\n      French\n   "
      },
      {
        "_text": "\n      Spanish\n   "
      }
    ]
  }
}
```

*原为发表于*[*codingbeautydev.com*](https://cbdev.link/a6ba4c)

# JavaScript 做的每一件疯狂的事情

JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**签约**](https://cbdev.link/d3c4eb) 并立即获得免费拷贝。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***