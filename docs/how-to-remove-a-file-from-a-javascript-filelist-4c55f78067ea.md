# 如何从 JavaScript 文件列表中删除文件？

> 原文：<https://javascript.plainenglish.io/how-to-remove-a-file-from-a-javascript-filelist-4c55f78067ea?source=collection_archive---------0----------------------->

![](img/60968a159c5f59a64b726e8b6d6839d8.png)

Photo by [kevin laminto](https://unsplash.com/@kxvn_lx?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想从 JavaScript 文件列表对象中删除一个文件。

在本文中，我们将研究如何从 JavaScript 文件列表对象中移除文件。

# 使用扩展运算符

从 JavaScript 文件列表中删除文件的一种方法是使用 spread 操作符将文件列表转换为数组。

然后我们可以调用`splice`来删除我们想要的文件。

例如，我们可以编写以下 HTML:

```
<input type='file' multiple id='files'>
```

我们添加`multiple`让选择多个文件。

然后，我们可以通过编写以下内容来删除选择的项目之一:

```
const input = document.getElementById('files')
input.addEventListener('change', () => {
  const fileListArr = [...input.files]
  fileListArr.splice(1, 1)
  console.log(fileListArr)
})
```

我们用`getElementById`得到文件输入元素。

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) **

## **希望扩大你的科技创业公司的知名度和采用率吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。**

**我们将`input.files`展开成一个数组。**

**然后，我们调用数组上的`splice`,将索引 1 作为第一个参数，并指定用第二个参数移除 1 个项目。**

**因此，`fileListArr`列出了第 1 和第 3 档。**

# **使用 Array.from 方法**

**我们可以用`Array.from`方法代替 spread 操作符。**

**例如，我们可以写:**

```
**<input type='file' multiple id='files'>**
```

**并且:**

```
**const input = document.getElementById('files')
input.addEventListener('change', () => {
  const fileListArr = Array.from(input.files)
  fileListArr.splice(1, 1)
  console.log(fileListArr)
})**
```

**做同样的事情。**

**唯一的区别是 spread 操作符被替换为`Array.from`。**

# **结论**

**从 JavaScript 文件列表中删除文件的一种方法是使用 spread 操作符将文件列表转换为数组。**

**同样，我们可以用`Array.from`方法代替 spread 操作符。**