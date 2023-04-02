# HeadlessUI- Listbox—安装必要的软件包&一个基本示例

> 原文：<https://javascript.plainenglish.io/headlessui-listbox-part-1-install-necessary-packages-and-basic-example-6fadbc7c83fd?source=collection_archive---------4----------------------->

## 第 1 部分:用 HeadlessUI 和 Next.js 创建一个 Listbox

在我们创建了 Next.js 项目之后，我们需要安装 Headless UI 和 Tailwind CSS。

安装无头用户界面:

```
yarn add @headlessui/react
```

安装顺风 CSS:

```
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

配置您的模板路径:

```
module.exports = {
  content: [
    "./pages/**/*.{js,ts,jsx,tsx}",
    "./components/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

将顺风指令添加到 CSS 中:

```
[@tailwind](http://twitter.com/tailwind) base;
[@tailwind](http://twitter.com/tailwind) components;
[@tailwind](http://twitter.com/tailwind) utilities;
```

我们只是从[文档](https://headlessui.dev/react/listbox)中复制示例代码，除了我们将类添加到列表框按钮和列表框选项中。

```
import { useState } from 'react'import { Listbox } from '@headlessui/react'const people = [{ id: 1, name: 'Durward Reynolds', unavailable: false },{ id: 2, name: 'Kenton Towne', unavailable: false },{ id: 3, name: 'Therese Wunsch', unavailable: false },{ id: 4, name: 'Benedict Kessler', unavailable: true },{ id: 5, name: 'Katelyn Rohan', unavailable: false },]export default function MyListbox() {const [selectedPerson, setSelectedPerson] = useState(people[0])return (<div className="fixed top-16 w-72 left-16"><Listbox value={selectedPerson} onChange={setSelectedPerson}>**<Listbox.Button  className="relative w-full cursor-default rounded-lg bg-white py-2 pl-3 pr-10 text-left shadow-md focus:outline-none focus-visible:border-indigo-500 focus-visible:ring-2 focus-visible:ring-white focus-visible:ring-opacity-75 focus-visible:ring-offset-2 focus-visible:ring-offset-orange-300 sm:text-sm">{selectedPerson.name}</Listbox.Button>****<Listbox.Options className="absolute mt-1 max-h-60 w-full overflow-auto rounded-md bg-white py-1 text-base shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none sm:text-sm">**{people.map((person) => (<Listbox.Optionkey={person.id}value={person}disabled={person.unavailable}>{person.name}</Listbox.Option>))}</Listbox.Options></Listbox></div>)}
```

我们还为 index.js 添加了背景色:

```
import MyListbox from '../components/MyListbox'export default function Home() {return (<div className="**bg-indigo-500 h-screen**"><MyListbox/></div>)}
```

![](img/a31c6353091e0c400f3aab3544abf0fb.png)

如果你喜欢这个故事，你可能也喜欢中等会员。一个月才 5 美元(一杯咖啡的价格！)但是它会在支持你最喜欢的作家的同时，给你无限的接触故事的机会。如果你注册使用[这个链接](https://ckmobile.medium.com/membership)，我会赚一小笔佣金。谢谢！

关注我们: [YouTube](https://www.youtube.com/channel/UCu4-4FnutvSHVo9WHvq80Ww?sub_confirmation=1) ， [Medium](https://ckmobile.medium.com/) ， [Udemy](https://www.udemy.com/user/cyruschan2/) ， [Linkedin](https://www.linkedin.com/company/ckmobi/) ， [Twitter](https://twitter.com/ckmobilejavasc1) ， [Instagram](https://www.instagram.com/ckmobile8050) ， [Gumroad](https://app.gumroad.com/ckmobile) ， [Quora](https://ckmobile.quora.com/) ， [Telegram](https://t.me/ckmobi)

加入分支机构赚钱

[](https://ckmobile.gumroad.com/affiliates) [## Gumroad

### 编辑描述

ckmobile.gumroad.com](https://ckmobile.gumroad.com/affiliates) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***