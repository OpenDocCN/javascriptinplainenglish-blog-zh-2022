# 如何使用 JavaScript 跳转到锚元素？

> 原文：<https://javascript.plainenglish.io/how-to-jump-to-an-anchor-element-by-using-javascript-5116c4b84493?source=collection_archive---------10----------------------->

![](img/8824016bfcfae957d0e73cb8f1d2191f.png)

Photo by [Anthony Fomin](https://unsplash.com/@aginsbrook?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想通过使用 JavaScript 跳转到一个锚元素。

在本文中，我们将看看如何使用 JavaScript 跳转到锚元素。

# 使用 location.href 和 history.replaceState

我们可以使用`location.href`属性来获得没有散列的 URL。

然后我们可以把散列附加到它上面。

然后我们可以用`history.replaceState`从地址栏中的 URL 中移除哈希。

例如，我们可以编写以下 HTML:

```
<button>
  jump
</button>
<div id='a'>
  Lorem ipsum dolor sit amet, consectetur adipiscing elit. Morbi rhoncus dignissim lacus, ac ullamcorper ex aliquam vel. Donec nec luctus augue, sit amet porttitor diam. Ut sit amet mi ac risus congue ultricies. Donec et condimentum nisi, sit amet consequat felis. Nam velit nibh, blandit non nunc eget, ullamcorper suscipit ex.
</div>
<div id='b'>
  Phasellus faucibus fringilla ullamcorper. Vivamus gravida urna vel odio rutrum rutrum. Vivamus pretium, orci eget cursus tempus, quam elit rutrum est, vel fermentum sapien odio sit amet velit. Etiam cursus pulvinar massa, non maximus dolor vestibulum id. Morbi mi mauris, iaculis ac sem a, porta vehicula risus. Curabitur tincidunt sollicitudin sapien, ac tristique ligula ullamcorper eget. Donec tincidunt orci non ligula auctor ullamcorper. Aliquam mattis elit mauris, at posuere nulla lobortis id.
</div>
```

然后我们可以添加一个按钮，通过编写以下代码向下滚动到 ID 为`b`的 div:

```
const jump = (h) => {
  const url = location.href;
  location.href = "#" + h;
  history.replaceState(null, null, url);
}const button = document.querySelector('button')
button.addEventListener('click', () => {
  jump('b')
})
```

我们有带`h`参数的`jump`函数，参数是我们想要滚动到的元素的 ID。

接下来，我们用`location.href`获取当前 URL。

然后，我们将 ID 为`h`的散列添加到其中，以跳转到 ID 为`h`的元素。

然后我们用第三个参数`url`调用`history.replaceState`，用原始的 URL 替换散列 URL。

接下来，我们用`document.querySelector`得到按钮。

然后我们用`'click'`调用`addEventListener`来添加一个点击监听器。

第二个参数是 click 监听器，它使用`'b'`调用`jump`来滚动到 ID 为`b`的 div。

# 结论

我们可以使用`location.href`属性来获取没有散列的 URL。

然后我们可以把散列附加到它上面。

然后我们可以用`history.replaceState`从地址栏的 URL 中移除哈希。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)**和* [***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****