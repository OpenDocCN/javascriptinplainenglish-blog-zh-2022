# 使用 JavaScript 将时间从 AM/PM 转换为 24 小时制

> 原文：<https://javascript.plainenglish.io/javascript-tutorial-convert-time-am-pm-to-24-hours-7a1bb69b20a?source=collection_archive---------4----------------------->

## 使用 JavaScript 将时间从 AM/PM 转换为 24 小时制的教程。

![](img/e6bcf4a814f3e1aa6bd2cf0c30ebe66f.png)

你好，朋友们你们好吗，希望你们永远健康成功。

这次我只想分享如何将上午或下午时间转换为 24 小时的 JavaScript 代码，希望这篇教程对你们所有人都有用。

好吧，这次就直接上教程吧。

```
var hrs = Number(timestart.match(/^(\d+)/)[1]);
 var mnts = Number(timestart.match(/:(\d+)/)[1]);
 var format = timestart.match(/\s(.*)$/)[1];
     if (format == "PM" && hrs < 12) hrs = hrs + 12;
     if (format == "AM" && hrs == 12) hrs = hrs - 12;
        var hours = hrs.toString();
        var minutes = mnts.toString();
            if (hrs < 10) hours = "0" + hours;
            if (mnts < 10) minutes = "0" + minutes;
            var timeend = hours + ":" + minutes + ":00";
            console.log(timeend); //h:i:s
```

如果我们看看上面的代码，它会将 am/pm 格式更改为 24 小时制。

```
var hrs = Number(timestart.match(/^(\d+)/)[1]);
 var mnts = Number(timestart.match(/:(\d+)/)[1]);
```

我们看上面的代码，我们将创建两个变量，即小时和分钟，接下来，我们将创建条件。

```
if (format == "PM" && hrs < 12) hrs = hrs + 12;
     if (format == "AM" && hrs == 12) hrs = hrs - 12;
```

上面的代码是在创建条件时创建条件的代码，接下来，我们将把小时和分钟分开。

```
if (hrs < 10) hours = "0" + hours;
  if (mnts < 10) minutes = "0" + minutes;
  var times = hours + ":" + minutes + ":00";
```

我们将得到 24 小时制的时间。

# 将 24 小时制时间转换为上午/下午

我们将把 24 小时时间格式改回 am/pm。这是要变回以前格式的代码。

```
d = new Date(times);  
var timerfix = d.getHours() + ':' + d.getMinutes();

  timerfix = timerfix.toString ().match (/^([01]\d|2[0-3])(:)([0-5]\d)(:[0-5]\d)?$/) || [timerfix];

  if (timerfix.length > 1) { // If time format correct
      timerfix = timerfix.slice (1);  // Remove full string match value
      timerfix[5] = +timerfix[0] < 12 ? ' AM' : ' PM'; // Set AM/PM
      timerfix[0] = +timerfix[0] % 12 || 12; // Adjust hours
  }

  console.log(timerfix.join(''));
```

我们会得到那个代码的小时和分钟。

```
var timerfix = d.getHours() + ':' + d.getMinutes();
```

接下来，我们将代码改为 string 类型。

```
timerfix = timerfix.toString ().match (/^([01]\d|2[0-3])(:)([0-5]\d)(:[0-5]\d)?$/) || [timerfix];
```

得到字符串格式的时间后，我们就可以求解条件。

```
if (timerfix.length > 1) { // If time format correct
      timerfix = timerfix.slice (1);  // Remove full string match value
      timerfix[5] = +timerfix[0] < 12 ? ' AM' : ' PM'; // Set AM/PM
      timerfix[0] = +timerfix[0] % 12 || 12; // Adjust hours
  }
```

然后，我们将以 am/pm 格式获取时间。

希望这篇教程对你们所有人都有用。这是一个简单的代码，有时我们会忘记如何使用它。

谢了。

来源:[https://temanngoding . com/tutorial-JavaScript-convert-waktu-am-pm-to-24-jam/](https://temanngoding.com/tutorial-javascript-convert-waktu-am-pm-to-24-jam/)

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *，加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***