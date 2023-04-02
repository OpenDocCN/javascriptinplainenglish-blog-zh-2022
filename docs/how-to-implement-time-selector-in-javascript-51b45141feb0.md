# 如何用 JavaScript 实现时间选择器

> 原文：<https://javascript.plainenglish.io/how-to-implement-time-selector-in-javascript-51b45141feb0?source=collection_archive---------13----------------------->

## JavaScript 中时间选择器的实现指南。

![](img/d633d2af3b3dff6486e8f2decc318f58.png)

```
This article mainly introduces the JS implementation of time selector in detail. The sample code in the article is very detailed and has certain reference value. Interested friends can refer to it.
```

本文中的例子分享了 JS 实现时间选择器的具体代码，供大家参考。具体内容如下:

## dateTime.js

```
function withData(param) {
  return param < 10 ? '0' + param : '' + param;
}
function getLoopArray(start, end) {
  var start = start || 0;
  var end = end || 1;
  var array = [];
  for (var i = start; i <= end; i++) {
    array.push(withData(i));
  }
  return array;
}
function getMonthDay(year, month) {
  var flag = year % 400 == 0 || (year % 4 == 0 && year % 100 != 0), array = null;switch (month) {
    case '01':
    case '03':
    case '05':
    case '07':
    case '08':
    case '10':
    case '12':
      array = getLoopArray(1, 31)
      break;
    case '04':
    case '06':
    case '09':
    case '11':
      array = getLoopArray(1, 30)
      break;
    case '02':
      array = flag ? getLoopArray(1, 29) : getLoopArray(1, 28)
      break;
    default:
      array = 'The month format is incorrect, please re-enter!'
  }
  return array;
}
function getNewDateArry() {
  // Processing of the current time
  var newDate = new Date();
  var year = withData(newDate.getFullYear()),
    mont = withData(newDate.getMonth() + 1),
    date = withData(newDate.getDate()),
    hour = withData(newDate.getHours()),
    minu = withData(newDate.getMinutes()),
    seco = withData(newDate.getSeconds());return [year, mont, date, hour, minu, seco];
}
function dateTimePicker(startYear, endYear, date) {
  // Returns the declaration of the default displayed array and linked array
  var dateTime = [], dateTimeArray = [[], [], [], [], [], []];
  var start = startYear || 1978;
  var end = endYear || 2100;
  // Start displaying data by default
  var defaultDate = date ? [...date.split(' ')[0].split('-'), ...date.split(' ')[1].split(':')] : getNewDateArry();
  // Process linkage list data
  /*year month day hours minutes seconds*/
  dateTimeArray[0] = getLoopArray(start, end);
  dateTimeArray[1] = getLoopArray(1, 12);
  dateTimeArray[2] = getMonthDay(defaultDate[0], defaultDate[1]);
  dateTimeArray[3] = getLoopArray(0, 23);
  dateTimeArray[4] = getLoopArray(0, 59);
  dateTimeArray[5] = getLoopArray(0, 59);dateTimeArray.forEach((current, index) => {
    dateTime.push(current.indexOf(defaultDate[index]));
  });  return {
    dateTimeArray: dateTimeArray,
    dateTime: dateTime
  }
}
```

## 实现示例

```
<!DOCTYPE html><html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Index</title>

   <!-- quote dateTimePicker.js -->
    <script src="~/Scripts/dateTime.js"></script>

    <script>
        window.onload = function () {
            var stryear = 2000;    //set start time 2000
             var endyear = 2060;    //Set end time 2060
            var date = dateTimePicker(stryear,endyear);    //Call the dateTimePicker method to get the time (start time, end time）//define datetime
            var year = date.dateTimeArray[0];    //year
            var month = date.dateTimeArray[1];//month
            var day = date.dateTimeArray[2];//day
            var time = date.dateTimeArray[3];//time
            var minute = date.dateTimeArray[4];//minute
            var second = date.dateTimeArray[5];//second//Put the date and time into the corresponding select
            var yearInner = "";
            var monthInner = "";
            var dayInner = "";
            var timeInner = "";
            var minuteInner = "";
            var secondInner = "";
            //year
            for (var i = 0; i < year.length; i++) {
                yearInner += '<option>' + year[i] + '</option>'
            }
            document.getElementById("yearSelect").innerHTML = yearInner;
            //month
            for (var i = 0; i < month.length; i++) {
                monthInner += '<option>' + month[i] + '</option>'
            }
            document.getElementById("monthSelect").innerHTML = monthInner;
            //day
            for (var i = 0; i < day.length; i++) {
                dayInner += '<option>' + day[i] + '</option>'
            }
            document.getElementById("daySelect").innerHTML = dayInner;
            //time
            for (var i = 0; i < time.length; i++) {
                timeInner += '<option>' + time[i] + '</option>'
            }
            document.getElementById("timeSelect").innerHTML = timeInner;
            //minute
            for (var i = 0; i < minute.length; i++) {
                minuteInner += '<option>' + minute[i] + '</option>'
            }
            document.getElementById("minuteSelect").innerHTML = minuteInner;
            //second
            for (var i = 0; i < second.length; i++) {
                secondInner += '<option>' + second[i] + '</option>'
            }
            document.getElementById("secondSelect").innerHTML = secondInner;
        }
    </script>
</head>
<body>
   <div>
      <select id="yearSelect"></select>
       <span>-</span>
       <select id="monthSelect"></select>
       <span>-</span>
       <select id="daySelect"></select>
       <br />
       <select id="timeSelect"></select>
       <span>:</span>
       <select id="minuteSelect"></select>
       <span>:</span>
       <select id="secondSelect"></select>
   </div>
</body>
</html>
```

以上是本文的全部内容，希望对你的学习有所帮助。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***