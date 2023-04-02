# HeadlessUI-过渡第 2 部分-显示和隐藏内容

> 原文：<https://javascript.plainenglish.io/headlessui-transitions-part-2-showing-and-hiding-content-a105a01b2c13?source=collection_archive---------4----------------------->

默认情况下，<transition>组件呈现为</transition>

，但是我们也可以使用`as` prop 将它呈现为其他元素。

我们可以在页面下创建 about.js。

![](img/9ad00c70c7831ec5306f7712e35cf1d2.png)

Photo by [Sora Sagano](https://unsplash.com/@sorasagano?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

```
 import React from 'react'const about = () => {return (<div>about</div>)}export default about
```

在 MyComponent.js 中，添加 as="a "以呈现为，链接到 about 页面

```
import { Transition } from '@headlessui/react'import React, {useState} from 'react'const MyComponent = () => {const [isShowing, setIsShowing] = useState(false);return (<><button className="absolute top-2 " onClick={() => setIsShowing((isShowing) => !isShowing)}>Toggle</button>**<Transition show={isShowing} as="a" href="/about">Go to about page.</Transition>**</>)}export default MyComponent
```

![](img/383be218ed6b6136c1cd778e9006271b.png)

如果你喜欢这个故事，你可能也喜欢中等会员。一个月才 5 美元(一杯咖啡的价格！)但是它会在支持你最喜欢的作家的同时，给你无限的接触故事的机会。如果你注册使用[这个链接](https://ckmobile.medium.com/membership)，我会赚一小笔佣金。谢谢！

关注我们: [YouTube](https://www.youtube.com/channel/UCu4-4FnutvSHVo9WHvq80Ww?sub_confirmation=1) ， [Medium](https://ckmobile.medium.com/) ， [Udemy](https://www.udemy.com/user/cyruschan2/) ， [Linkedin](https://www.linkedin.com/company/ckmobi/) ， [Twitter](https://twitter.com/ckmobilejavasc1) ， [Instagram](https://www.instagram.com/ckmobile8050) ， [Gumroad](https://app.gumroad.com/ckmobile) ， [Quora](https://ckmobile.quora.com/) ， [Telegram](https://t.me/ckmobi)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)**和* [***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****