# 如何在 Node.js 中将 JSON 转换成 XML

> 原文：<https://javascript.plainenglish.io/node-js-convert-json-to-xml-137e41b2acbb?source=collection_archive---------8----------------------->

## 了解如何在 Node.js 中将 JSON 轻松转换为 XML。

![](img/70d0a7b5b513265bd8beee46cb131474.png)

我们可以在 Node.js 中使用`xml-js`库轻松地将 JSON 字符串转换成 XML 字符串。

```
import { json2xml } from 'xml-js';const jsonObj = {
  name: 'Garage',
  cars: [
    { color: 'red', maxSpeed: 120, age: 2 },
    { color: 'blue', maxSpeed: 100, age: 3 },
    { color: 'green', maxSpeed: 130, age: 2 },
  ],
};const json = JSON.stringify(jsonObj);const xml = json2xml(json, { compact: true, spaces: 4 });console.log(xml);
```

该代码将有以下输出:

```
<name>Garage</name>
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
</cars>
```

# 安装 xml-js

在使用`xml-js`之前，我们需要将它安装到我们的项目中。我们可以使用 NPM 命令行界面来实现这一点。

```
npm i xml-js
```

或使用纱线 CLI:

```
yarn add xml-js
```

安装完成后，我们可以将其导入 JavaScript 模块，如下所示:

```
import { json2xml } from 'xml-js';
```

我们使用导入析构直接从库中访问`json2xml()`方法。

对于 CommonJS 模块，我们将改为这样导入它:

```
const { json2xml } = require('xml-js');
```

# `json2xml()`功能

库中的`json2xml()`函数有两个参数。第一个是要转换成 XML 的 JSON 字符串，第二个是对象。

```
const xml = json2xml(json, { compact: true, spaces: 4 });
```

# 在 Node.js 中自定义 JSON 到 XML 的转换

此对象用于指定自定义转换过程的各种选项。

在我们的示例中，我们将`compact`属性设置为`true`，以表明 JSON 字符串输入是紧凑形式的。

我们将`spaces`属性设置为`4`，将嵌套的 XML 节点缩进 4 个空格。因此，我们可以通过将`spaces`设置为`1`来减少缩进:

```
import { json2xml } from 'xml-js';const jsonObj = {
  name: 'Garage',
  cars: [
    { color: 'red', maxSpeed: 120, age: 2 },
    { color: 'blue', maxSpeed: 100, age: 3 },
    { color: 'green', maxSpeed: 130, age: 2 },
  ],
};const json = JSON.stringify(jsonObj);const xml = json2xml(json, { compact: true, spaces: 1 });console.log(xml);
```

现在，我们将得到以下 XML 输出:

```
<name>Garage</name>
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
</cars>
```

# Node.js 中 JSON 到 XML 的本机转换

如果不想使用任何第三方库，那么可以在 Node.js 中使用这个递归函数将 JSON 转换成 XML。

```
function JSONtoXML(obj) {
  let xml = '';
  for (let prop in obj) {
    xml += obj[prop] instanceof Array ? '' : '<' + prop + '>';
    if (obj[prop] instanceof Array) {
      for (let array in obj[prop]) {
        xml += '\n<' + prop + '>\n';
        xml += JSONtoXML(new Object(obj[prop][array]));
        xml += '</' + prop + '>';
      }
    } else if (typeof obj[prop] == 'object') {
      xml += JSONtoXML(new Object(obj[prop]));
    } else {
      xml += obj[prop];
    }
    xml += obj[prop] instanceof Array ? '' : '</' + prop + '>\n';
  }
  xml = xml.replace(/<\/?[0-9]{1,}>/g, '');
  return xml;
}const jsonObj = {
  name: 'Garage',
  cars: [
    { color: 'red', maxSpeed: 120, age: 2 },
    { color: 'blue', maxSpeed: 100, age: 3 },
    { color: 'green', maxSpeed: 130, age: 2 },
  ],
};const xml = JSONtoXML(jsonObj);console.log(xml);
```

该代码将产生以下输出:

```
<name>Garage</name><cars>
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
</cars>
```

*原载于*[*codingbeautydev.com*](https://cbdev.link/fe37fc)

# JavaScript 做的每一件疯狂的事情

一本关于 JavaScript 微妙的警告和鲜为人知的部分的迷人指南。

![](img/143ee152ba78025ea8643ba5b9726a20.png)

[**报名**](https://cbdev.link/d3c4eb) 立即免费领取一份。