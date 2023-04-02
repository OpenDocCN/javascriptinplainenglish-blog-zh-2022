# 如何用 JavaScript 买车

> 原文：<https://javascript.plainenglish.io/how-to-buy-a-car-with-javascript-ca2809fc0db5?source=collection_archive---------11----------------------->

## 毁灭 2022

## 不是在现实中，而是为了解决一个灾难性的 2022 问题

![](img/62530ccdf9085aff802cde722e113816.png)

今天的《毁灭 2022》特别有趣。它本身并不复杂，只是计算两条曲线的交点。最有趣的事情是折射结果。不过还是从问题的正文开始吧。

# 问题:买车

链接到[形](https://www.codewars.com/kata/554a44516729e4d80b000012)

一个男人有一辆相当旧的车，值得买。他看到一辆二手车值`$8000`。他想保留他的旧车，直到他能买到二手车。

他认为他每个月可以节省 1000 美元，但是他的旧车和新车的价格每个月下降了`1.5`%。此外，在每两个月结束时，这一损失百分比会增加`0.5`个百分点。我们的人发现做这些计算很困难。

你能帮助他吗？

他需要多少个月才能攒够钱买他想要的车，他还会剩下多少钱？

**参数和函数返回:**

```
parameter (positive int or float, guaranteed) start_price_old (Old car price)
parameter (positive int or float, guaranteed) start_price_new (New car price)
parameter (positive int or float, guaranteed) saving_per_month
parameter (positive float or int, guaranteed) percent_loss_by_month

nbMonths(2000, 8000, 1000, 1.5) should return [6, 766] or (6, 766)
```

**上述示例的详细信息:**

```
end month 1: percent_loss 1.5 available -4910.0
end month 2: percent_loss 2.0 available -3791.7999...
end month 3: percent_loss 2.0 available -2675.964
end month 4: percent_loss 2.5 available -1534.06489...
end month 5: percent_loss 2.5 available -395.71327...
end month 6: percent_loss 3.0 available 766.158120825...
return [6, 766] or (6, 766)
```

其中`6`是在**结束时**他可以购买新车的月数，而`766`是最接近`766.158...`的整数(四舍五入`766.158`得到`766`)。

**注:**

销售、购买和储蓄通常在月末进行。计算在每个月的月底进行，但是如果从一开始就偶然发现旧车的价值大于新车的价值或者相等，则没有节省，不需要等待，因此他可以在月初购买新车:

```
nbMonths(12000, 8000, 1000, 1.5) should return [0, 4000]
nbMonths(8000, 8000, 1000, 1.5) should return [0, 0]
```

我们不处理银行储蓄存款:-)

# 我的解决方案

![](img/64f9038ac2c0c7858599a482c28aeff6.png)

解决方案大概是这样的:

```
export function nbMonths(p) {
  while (getMoneyLeft(p) < 0) {
    p = { ...updateValues(p) };
  }

  return [p.month, Math.round(getMoneyLeft(p))];
}
```

如果我们愿意，我们可以使用递归函数:

```
export function nbMonths(p) {
  const moneyLeft = getMoneyLeft(p);

  if (moneyLeft >= 0) {
    return [p.month, Math.round(getMoneyLeft(p))];
  } else {
    return nbMonths(updateValues(p));
  }
}
```

显然，这些解决方案使用了其他功能。我决定把这个问题分成几个单独的函数，从概念上简化它。

这是一个编程选择。就我个人而言，我更喜欢使用简单的功能，并将其作为乐高积木来构建更大的东西。在这种情况下，没有必要。无需拆分代码，解决方案如下:

```
export function nbMonths(
  priceOld: number,
  priceNew: number,
  saving: number,
  percentLoss: number
): number[] {
  let available: number = 0;
  let month: number = 0;

  while (available + priceOld < priceNew) {
    month++;
    percentLoss += month % 2 == 0 ? 0.5 : 0;
    priceNew *= (100 - percentLoss) / 100;
    priceOld *= (100 - percentLoss) / 100;
    available += saving;
  }

  return [month, Math.round(available + priceOld - priceNew)];
}
```

但是这段代码中有我不喜欢的地方。而且是参数的问题。这是一个有太多参数的函数。在这种情况下，我更喜欢使用一个对象:

```
type Param = {
  priceOld: number;
  priceNew: number;
  saving: number;
  percentLoss: number;
  month: number;
};
```

然后我开始把问题分成几部分。首先，我需要一个函数来计算两辆汽车的更新价格。

```
const value = (price: number, delta: number): number =>
  price * (1 - delta / 100);

const updatePriceNew = (p: Param): number => value(p.priceNew, p.percentLoss);
const updatePriceOld = (p: Param): number => value(p.priceOld, p.percentLoss);
```

接下来，我需要更新损坏率的东西。因为它每两个月发生一次，所以我可以检查该月是否是偶数:

```
const updatePercentLoss = (p: Param): number =>
  p.percentLoss + (1 - (p.month % 2)) * 0.5;
```

更新月份号非常简单:

```
const updateMonth = (p: Param): number => p.month + 1;
```

我还需要一个函数来计算购买后剩下的钱。这样，如果价值为负，我知道我们还买不起这辆车。

```
const getMoneyLeft = (p: Param): number =>
  p.month * p.saving + p.priceOld - p.priceNew;
```

我现在有了解决这个问题所需的所有部件。

```
export function nbMonths(
  priceOld: number,
  priceNew: number,
  saving: number,
  percentLoss: number,
  month: number = 0
): number[] {
  let p: Param = { priceOld, priceNew, saving, percentLoss, month };

  while (getMoneyLeft(p) < 0) {
    p.month = updateMonth(p);
    p.percentLoss = updatePercentLoss(p);
    p.priceNew = updatePriceNew(p);
    p.priceOld = updatePriceOld(p);
  }

  return [p.month, Math.round(getMoneyLeft(p))];
}
```

如果我们想做过头，我们可以增加一个新功能:

```
const updateValues = (p: Param): Param => {
  return {
    priceOld: updatePriceOld(p),
    priceNew: updatePriceNew(p),
    saving: p.saving,
    percentLoss: updatePercentLoss(p),
    month: updateMonth(p),
  };
};
```

这让我们回到最初的解决方案。将各个部分放在一起，并使代码适应 [CodeWars](https://www.codewars.com/) 测试，我们得到:

```
type Param = {
  priceOld: number;
  priceNew: number;
  saving: number;
  percentLoss: number;
  month: number;
};

const value = (price: number, delta: number): number =>
  price * (1 - delta / 100);

const updatePercentLoss = (p: Param): number =>
  p.percentLoss + (1 - (p.month % 2)) * 0.5;
const updatePriceNew = (p: Param): number => value(p.priceNew, p.percentLoss);
const updatePriceOld = (p: Param): number => value(p.priceOld, p.percentLoss);
const updateMonth = (p: Param): number => p.month + 1;

const getMoneyLeft = (p: Param): number =>
  p.month * p.saving + p.priceOld - p.priceNew;

const updateValues = (p: Param): Param => {
  return {
    priceOld: updatePriceOld(p),
    priceNew: updatePriceNew(p),
    saving: p.saving,
    percentLoss: updatePercentLoss(p),
    month: updateMonth(p),
  };
};

export function nbMonths(
  priceOld: number,
  priceNew: number,
  saving: number,
  percentLoss: number,
  month: number = 0
): number[] {
  let p: Param = { priceOld, priceNew, saving, percentLoss, month };

  while (getMoneyLeft(p) < 0) {
    p = { ...updateValues(p) };
  }

  return [p.month, Math.round(getMoneyLeft(p))];
}
```

感谢阅读！敬请关注更多内容。

***不要错过我的下一篇文章—报名我的*** [***中邮箱列表***](https://medium.com/subscribe/@el3um4s)

[](https://el3um4s.medium.com/membership) [## 通过我的推荐链接加入 Medium—Samuele

### 阅读萨缪尔的每一个故事(以及媒体上成千上万的其他作家)。不是中等会员？在这里加入一块…

el3um4s.medium.com](https://el3um4s.medium.com/membership) 

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

***有兴趣缩放你的软件启动*** *？检查出* [***电路***](https://circuit.ooo/?utm=publication-post-cta) *。*