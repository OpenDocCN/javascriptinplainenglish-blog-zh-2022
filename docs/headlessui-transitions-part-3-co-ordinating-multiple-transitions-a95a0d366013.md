# HeadlessUI-过渡第 3 部分-协调多个过渡

> 原文：<https://javascript.plainenglish.io/headlessui-transitions-part-3-co-ordinating-multiple-transitions-a95a0d366013?source=collection_archive---------3----------------------->

![](img/62b4feaba4329e645a1eeeba08f0508d.png)

Photo by [Austin Poon](https://unsplash.com/@austinpoon?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时需要在不同元素上进行转换。一个例子是当侧边栏滑入时，下面会出现一个黑色的覆盖层。

在本文中，我们将制作一个简单的来演示它。

首先，转到“components”文件夹并创建 Sidebar.js。

```
import { Transition } from '@headlessui/react'import React, { useState } from 'react'const Sidebar = () => {const [isShowing, setIsShowing] = useState(false);return (<div className="w-full"><button className="absolute top-2 " onClick={() => setIsShowing((isShowing) => !isShowing)}>Toggle</button><Transition show={isShowing}>{/* Background overlay */}<Transition.Childenter="transition-opacity ease-linear duration-300"enterFrom="opacity-0"enterTo="opacity-100"leave="transition-opacity ease-linear duration-300"leaveFrom="opacity-100"leaveTo="opacity-0">{/* ... */}<div className="h-screen w-full bg-black opacity-50">black</div></Transition.Child>{/* Sliding sidebar */}<div className="fixed inset-0 overflow-y-auto"><div className="flex min-h-full items-center justify-center p-4 text-center"><Transition.Childenter="transition ease-in-out duration-300 transform"enterFrom="-translate-x-full"enterTo="translate-x-0"leave="transition ease-in-out duration-300 transform"leaveFrom="translate-x-0"leaveTo="-translate-x-full"><div className="bg-white rounded-md w-max p-5 " onClick={() => setIsShowing(false)}>sidebar</div></Transition.Child></div></div></Transition></div>)}export default Sidebar
```

在[文档](https://headlessui.dev/react/transition)中，有一个关于协调多个过渡的例子，我们复制并填充`{/*...*/}`

第一个

是创建一个黑色叠加。

```
<div className="h-screen w-full bg-black opacity-50">black</div>
```

第二部分是创建一个小侧边栏，放在屏幕中央。我们还添加了一个 onClick 来设置点击时的`isShowing`为 false。

```
<div className="fixed inset-0 overflow-y-auto"><div className="flex min-h-full items-center justify-center p-4 text-center"><Transition.Childenter="transition ease-in-out duration-300 transform"enterFrom="-translate-x-full"enterTo="translate-x-0"leave="transition ease-in-out duration-300 transform"leaveFrom="translate-x-0"leaveTo="-translate-x-full"><div className="bg-white rounded-md w-max p-5 " onClick={() => setIsShowing(false)}>sidebar</div></Transition.Child></div></div>
```

![](img/0d57c99933a2b64f45807ec1f835fa86.png)

如果你喜欢这个故事，你可能也喜欢中等会员。一个月才 5 美元(一杯咖啡的价格！)但是它会在支持你最喜欢的作家的同时，给你无限的接触故事的机会。如果你注册使用[这个链接](https://ckmobile.medium.com/membership)，我会赚一小笔佣金。谢谢！

关注我们: [YouTube](https://www.youtube.com/channel/UCu4-4FnutvSHVo9WHvq80Ww?sub_confirmation=1) ， [Medium](https://ckmobile.medium.com/) ， [Udemy](https://www.udemy.com/user/cyruschan2/) ， [Linkedin](https://www.linkedin.com/company/ckmobi/) ， [Twitter](https://twitter.com/ckmobilejavasc1) ， [Instagram](https://www.instagram.com/ckmobile8050) ， [Gumroad](https://app.gumroad.com/ckmobile) ， [Quora](https://ckmobile.quora.com/) ， [Telegram](https://t.me/ckmobi)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)**和* [***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****