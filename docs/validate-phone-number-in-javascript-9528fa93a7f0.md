# 用 JavaScript 验证电话号码

> 原文：<https://javascript.plainenglish.io/validate-phone-number-in-javascript-9528fa93a7f0?source=collection_archive---------4----------------------->

![](img/a1fe52370782e9ee003c452615cb2c4c.png)

Photo by [Antoine Beauvillain](https://unsplash.com/it/@antoinebeauvillain?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在收集用户信息时，验证电话号码是一项重要任务。对于在线表单来说尤其如此，用户可能需要输入他们的电话号码来接收更新或通知。为了确保用户输入的电话号码是有效的，有必要使用验证方法。

使用 JavaScript 验证电话号码的一种方法是使用正则表达式，也称为 regex。正则表达式是一组字符，可用于匹配字符串中的模式。它们通常用于搜索、替换和验证数据。

要使用 JavaScript 和 regex 验证电话号码，我们可以使用以下代码:

```
function validatePhoneNumber(phoneNumber) {
  var regex = /^\(?([0-9]{3})\)?[-. ]?([0-9]{3})[-. ]?([0-9]{4})$/;
  if (regex.test(phoneNumber)) {
    return true;
  } else {
    return false;
  }
}
```

这段代码定义了一个名为“validatePhoneNumber”的函数，它接受一个电话号码作为参数。该函数使用正则表达式来测试电话号码是否与特定模式匹配。如果电话号码与模式匹配，该函数返回 true。如果不匹配，该函数将返回 false。

此函数中使用的正则表达式用于匹配以下格式的电话号码:(XXX) XXX-XXXX 或 XXX-XXX-XXXX。这意味着电话号码必须包含圆括号中的区号，后跟三位数的交换码和四位数的本地号码。

要使用这个函数，我们可以简单地调用它并传入一个电话号码作为参数，就像这样:

```
var phoneNumber = "(123) 456-7890";
if (validatePhoneNumber(phoneNumber)) {
  console.log("Valid phone number!");
} else {
  console.log("Invalid phone number!");
}
```

在本例中，电话号码“(123)456–7890”将被视为有效的电话号码，因为它与正则表达式中指定的模式相匹配。

需要注意的是，这种验证方法并不是绝对可靠的。例如，它不考虑带分机的电话号码或美国以外的电话号码。但是，它是基本电话号码验证的良好起点，可以修改以满足特定需求。

总之，JavaScript 和正则表达式可以用来以简单有效的方式验证电话号码。通过使用本文提供的代码，开发人员可以很容易地确保用户输入的电话号码是有效的格式。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。*

*报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *

****想看看你的软件启动规模*** *？检查* [***电路***](https://circuit.ooo/?utm=publication-post-cta) *。**