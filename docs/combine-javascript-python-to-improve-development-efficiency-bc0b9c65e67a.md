# 结合 JavaScript 和 Python 提高开发效率

> 原文：<https://javascript.plainenglish.io/combine-javascript-python-to-improve-development-efficiency-bc0b9c65e67a?source=collection_archive---------7----------------------->

## 完美结合 JavaScript 和 Python 高效解决工程问题的指南。

![](img/74fe365e510f75c96e926f52e399055b.png)

PHP，Python，Go，JavaScript…哪个是最好的编程语言？

每个人都有自己的答案，但是说到 web 开发，没有什么能打败 JavaScript。但有时我们不得不做要求更高的任务，比如分析大量数据。在这种情况下，Python 可能是更好的选择。但这只是我们网站的一个功能，自然也不会因为这个需求而用 Python 开发整个项目。

今天给大家介绍一种可以完美结合 JavaScript 和 Python 高效解决工程问题的方法。

## Python + JavaScript =牛逼！

我们可以使用 **Node.js** 中的子流程在需要时运行 Python 脚本。

```
**const result = require('subprocess').result,
app.get("process_data", (req, res) => {
   result('python3', ['demo.py'])
})**
```

编写另一个 Python 脚本:

```
***# demo.py*
doSometing()**
```

除了这种方式，我们还可以将数据传递给我们的 **Python 脚本**。

```
**const result = require('subprocess').result,
app.get("process_data", (req, res) => {
    const msg = "Hello World"
   result('python3', ['demo.py', msg])
})**
```

在 Python 中，为了能够读取数据，我们必须导入 **sys 模块**。

```
**import sys, json

def main():
    msg = sys.argv[1]
    doSometing(msg)

if __name__ == '__main__':
    main()**
```

现在，我们不是在生成 Python 流程时传递数据，而是在任务工作流中发送数据。

```
**const result = require('subprocess').result,
const py = result('python3', ['demo.py'])
const data = {
    msg: "Hello World"
}
py.stdin.write(JSON.stringify(data)) *//we have to send data as a string, so we are using JSON.stringify*
py.stdin.end()**
```

修改 Python 脚本:

```
**import sys, json

def main():
    lines = sys.stdin.readlines()
    data = json.loads(lines)
    doSometing(data['msg'])

if __name__ == '__main__':
    main()**
```

最后，我们可以从 **Python 脚本向 **Node.js** 发送响应。**

```
**const result = require('subprocess').result,
const py = result('python3', ['demo.py'])

py.stdout.on('data', function(res){
   let data = JSON.parse(res.toString())
   console.log(data)
})**
```

Python 代码是:

```
**import sys

*# You will have your own implementation of get data.In this case lets assume it returns a dict/json.*****res = getData()
print(json.dumps(data))

sys.stdout.flush()**
```

这样就可以在 **web 开发**的过程中兼顾 **JavaScript 和 Python** 的优势，最大限度的发挥不同编程语言的价值。不需要使用数据库或者开发繁琐的 **API** 结构，就可以将 JavaScript 和 Python 结合起来，提高开发效率。

***感谢您的阅读！***

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和**[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。**