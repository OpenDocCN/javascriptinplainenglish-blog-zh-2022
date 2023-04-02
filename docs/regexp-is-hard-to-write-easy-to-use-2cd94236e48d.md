# 正则表达式很难写，很容易使用

> 原文：<https://javascript.plainenglish.io/regexp-is-hard-to-write-easy-to-use-2cd94236e48d?source=collection_archive---------9----------------------->

## 10 个有用的正则表达式。

![](img/d45124c4b09827aeb9ce917f9920d583.png)

当你用 JavaScript 编码时，`RegExp`对你来说可能是一项艰苦的工作。虽然有很多教程和网站可以帮助你学习正则表达式，但是当你看到`(?!^)(?=(\\d{3})+`时，它看起来就像是外星文字一样。另一方面，做`verification`、 `string extraction`、`deformation`真的很容易。最好的是能够直接使用复制粘贴。

今天，我们来看看 10 个有用的正则表达式。

# 1.电子邮件验证

电子邮件验证是我们用户注册最常用的方法。

```
const checkEmailRegExp = /^([A-Za-z0-9_\-\.])+\@([A-Za-z0-9_\-\.])+\.([A-Za-z]{2,4})$/
console.log(checkEmailRegExp.test('[aabbcc@gmail.com](mailto:aabbcc@gmail.com)')) //true
console.log(checkEmailRegExp.test('aabbcc_gmail.com')) //false
console.log(checkEmailRegExp.test('aabbcc@gmail_com')) //false
console.log(checkEmailRegExp.test('aabbcc@'))          //false
console.log(checkEmailRegExp.test('@aabbcc'))          //false
```

# 2.十六进制颜色

确定十六进制颜色是否合法。

```
const checkHexColorRegExp = /^#?([a-fA-F0-9]{6}|[a-fA-F0-9]{3})$/console.log(checkHexColorRegExp.test('#fff'))     //true
console.log(checkHexColorRegExp.test('#808080'))  //true  console.log(checkHexColorRegExp.test('#ffff'))    //false
console.log(checkHexColorRegExp.test('#8080801')) //false
```

# 3.千位格式

在项目中，页面显示经常遇到的货币量。为了使金额的显示更加人性化和规范化，需要增加一个货币格式化策略。这就是所谓的千位格式化。

1.  `123456789` = > `123,456,789`
2.  `123456789.123` = > `123,456,789.123`

```
const toThousands = (price) => {   
return price.replace(new RegExp(`(?!^)(?=(\\d{3})+${price.includes('.') ? '\\.' : '$'})`, 'g'), ',')   
} 
toThousands('123456789')     // '123,456,789' toThousands('123456789.123') // '123,456,789.123' 
toThousands('123')           // '123'
```

# **4。日期格式**

`2022–06–29` = > `06/29/2022`

```
var regex = /(\d{4})-(\d{1,2})-(\d{1,2})/;
console.log("2022-06-29".replace(regex, "$2/$3/$1")); //'06/29/2022'
console.log("2022-6-9".replace(regex, "$2/$3/$1"));   //'9/6/2022'
```

# **5。修剪弦**

删除前导空格是很常见的。

```
let trim = (string) => {     
   return string.replace(/^\s+|\s+$/g, '') 
}
console.log(trim(' hello world ')) //hello world
console.log(trim(' hello world'))  //hello world
console.log(trim('hello world '))  //hello world
```

# 6.HTML 转义

防止 XSS 攻击的方法之一是执行 HTML 转义，即对应于符号的转义字符。

```
const escape = (string) => {
  const escapeMaps = {
    '&': 'amp',
    '<': 'lt',
    '>': 'gt',
    '"': 'quot',
    "'": '#39'
  }
  // The effect here is the same as that of /[&amp;<> "']/g
  const escapeRegexp = new RegExp(`[${Object.keys(escapeMaps).join('')}]`, 'g')
  return string.replace(escapeRegexp, (match) => `&${escapeMaps[match]};`)
}console.log(escape(`
  <div>
    <p>hello world</p>
  </div>
`))
/*
&lt;div&gt;
  &lt;p&gt;hello world&lt;/p&gt;
&lt;/div&gt;
*/
```

# 7.HTML 反向转义

HTML 转义的逆过程。

```
const unescape = (string) => {
  const unescapeMaps = {
    'amp': '&',
    'lt': '<',
    'gt': '>',
    'quot': '"',
    '#39': "'"
  }
  const unescapeRegexp = /&([^;]+);/g
  return string.replace(unescapeRegexp, (match, unescapeKey) => {
    return unescapeMaps[ unescapeKey ] || match
  })
}console.log(unescape(`
  &lt;div&gt;
    &lt;p&gt;hello world&lt;/p&gt;
  &lt;/div&gt;
`))
/*
<div>
  <p>hello world</p>
</div>
*/
```

# 8.解析链接参数

如何从该链接中获取参数值:

```
[https://www.google.com/search?q=reg&oq=ex](https://www.google.com/search?q=reg&oq=ex')const q = getQueryByName('q')  //reg
const oq = getQueryByName('oq') //ex
```

通过使用`RegExp`，你可以实现`getQueryByName`。

```
const url = '[https://www.google.com/search?q=reg&oq=ex'](https://www.google.com/search?q=reg&oq=ex')
const getQueryByName = (name) => {
  const queryNameRegex = new RegExp(`[?&]${name}=([^&]*)(&|$)`)
  const queryNameMatch = url.match(queryNameRegex)
  // Generally, it will be decoded by decodeURIComponent
  return queryNameMatch ? decodeURIComponent(queryNameMatch[1]) : ''
}const q = getQueryByName('q')
const oq = getQueryByName('oq')console.log(q, oq) // reg, ex
```

# 9.URL 验证

检查 URL 是否有效。

```
const regExp = /https?:\/\/(www\.)?[-a-zA-Z0-9@:%._\+~#=]{1,256}\.[a-zA-Z0-9()]{1,6}\b([-a-zA-Z0-9()!@:%_\+.~#?&\/\/=]*)/console.log(regExp.test('abcdef'))           //false
console.log(regExp.test('www.whatever.com')) //false
console.log(regExp.test('https://github.com/geongeorge/i-hate-regex'))                                     //true
console.log(checkUrlRegEx.test('https://www.facebook.com/')) //true
console.log(regExp.test('https://www.google.com/')) //true
console.log(regExp.test('https://xkcd.com/2293/'))  //true
console.log(regExp.test('https://this-shouldn\'t.match@example.com'))                     //false
console.log(regExp.test('http://www.example.com/')) //true
```

# 10.获取网页图像地址

这个需求可能会被爬虫更多的使用，定期使用来获取当前网页上所有图片的地址。尝试在控制台中打印它，它非常有用。

```
const matchImgs = (sHtml) => {
  const imgUrlRegex = /<img[^>]+src="((?:https?:)?\/\/[^"]+)"[^>]*?>/gi
  let matchImgUrls = []

  sHtml.replace(imgUrlRegex, (match, $1) => {
    $1 && matchImgUrls.push($1)
  })
  return matchImgUrls
}console.log(matchImgs(document.body.innerHTML))
```

# 最后

以上就是关于`RegExp`的全部内容，如果你觉得还不够，我给你推荐一个名为`[i Hate Regex](https://ihateregex.io/)`的正则表达式工具网站，它是一个在线开源工具，可以快速检索和匹配正确的正则表达式，帮助你完成`username`、`email`、`date`、`mobile phone number`、`password`等常用规则的验证。

[](https://ihateregex.io/) [## 我讨厌正则表达式-正则表达式备忘单

### 我讨厌正则表达式是一个正则表达式备忘单，它也解释了常用的表达式，以便你理解它。停下来…

ihateregex.io](https://ihateregex.io/) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*