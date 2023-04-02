# 验证电子邮件的 JS 正则表达式

> 原文：<https://javascript.plainenglish.io/js-regular-expression-to-verify-email-da4742e77b72?source=collection_archive---------11----------------------->

![](img/e7b227e9f9bcff7ebc89a2f3a8e24243.png)

```
<!DOCTYPE html>
<html lang="zh-CN">
<head>
 <meta charset="UTF-8">
 <title>Document</title>
</head>
<body>
 <input type="text" placeholder="please input your email" id="email">
</body>
<script>
 email.onchange = function(){
  var email = this.value;
  var reg = /^([a-zA-Z]|[0-9])(\w|\-)+@[a-zA-Z0-9]+\.([a-zA-Z]{2,4})$/;
  if(reg.test(email)){
   alert("Email format is correct");
  }else{
   alert("E-mail format is incorrect");
  }
 }
</script>
</html>
```

实现规则:
以数字或字母开头，中间的 k 后面是若干下划线或“-”，后面是“@”符号，后面是数字和字母。然后是“.”符号加 2-4 个字母。

*更多内容尽在* [***说白了. io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。*