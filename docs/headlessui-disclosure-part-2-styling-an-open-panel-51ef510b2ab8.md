# 披露

> 原文：<https://javascript.plainenglish.io/headlessui-disclosure-part-2-styling-an-open-panel-51ef510b2ab8?source=collection_archive---------11----------------------->

## 第 2 部分:设计开放面板的样式

![](img/79899a54517456b1db5b58d602727277.png)

Photo by [Christopher Gower](https://unsplash.com/@cgower?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在这一部分，我们将设计开放面板的样式。

首先，我们需要安装 react heroicon

```
npm i @heroicons/react
```

然后导入顶部的`ChevronUpIcon`。

```
import { ChevronUpIcon } from '@heroicons/react/solid'
```

然后我们在开放状态的帮助下有条件地改变状态。

```
{({open})=>(<></>)}
```

我们把所有的披露。按钮和披露。碎片里的面板。

```
<div className="w-full px-4 pt-16"><div className="mx-auto w-full max-w-md rounded-2xl bg-white p-2"><Disclosure>**{({ open }) => (**<><Disclosure.Button className="flex w-full justify-between rounded-lg bg-purple-100 px-4 py-2 text-left text-sm font-medium text-purple-900 hover:bg-purple-200 focus:outline-none focus-visible:ring focus-visible:ring-purple-500 focus-visible:ring-opacity-75"><span>Is team pricing available?</span>**<ChevronUpIcon****className={`${open ? 'rotate-180 transform' : ''****} h-5 w-5 text-purple-500`}****/>**</Disclosure.Button><Disclosure.Panel className="px-4 pt-4 pb-2 text-sm text-gray-500">Yes! You can purchase a license that you can share with your entireteam.</Disclosure.Panel></>)}</Disclosure></div></div>
```

如果你喜欢这个故事，你可能也喜欢中等会员。一个月才 5 美元(一杯咖啡的价格！)但是它会在支持你最喜欢的作家的同时，给你无限的接触故事的机会。如果你用[这个链接](https://ckmobile.medium.com/membership)注册，我会赚一小笔佣金。谢谢！

# 关注我们: [YouTube](https://www.youtube.com/channel/UCu4-4FnutvSHVo9WHvq80Ww?sub_confirmation=1) ， [Medium](https://ckmobile.medium.com/) ， [Udemy](https://www.udemy.com/user/cyruschan2/) ， [Linkedin](https://www.linkedin.com/company/ckmobi/) ， [Twitter](https://twitter.com/ckmobilejavasc1) ， [Instagram](https://www.instagram.com/ckmobile8050) ， [Gumroad](https://app.gumroad.com/ckmobile) ， [Quora](https://ckmobile.quora.com/) ， [Telegram](https://t.me/ckmobi)

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****