# 如何修复 jQuery 数据表的“无法读取未定义的属性样式”错误？

> 原文：<https://javascript.plainenglish.io/how-to-fix-the-cannot-read-property-style-of-undefined-error-with-jquery-datatables-7ad46cb0af4e?source=collection_archive---------1----------------------->

![](img/49bd61cfe8b797a7f1805c187e43f4e9.png)

Photo by [Priscilla Du Preez](https://unsplash.com/@priscilladupreez?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，当我们试图添加一个带有 jQuery 数据表的表时，我们会得到“无法读取未定义的属性样式”。

在本文中，当我们试图添加一个带有 jQuery 数据表的表时，我们将看到“无法读取未定义的属性样式”。

# th 元素不匹配

该错误的一个原因是表头或表尾中的`th`元素的数量与`columns`选项中定义的列不匹配。

因此，我们应该确保两者匹配。

# 列跨度不匹配

如果我们在表格标题中有`colspan`，我们应该确保至少有 2 个标题行，每列有一个唯一的`th`元素。

# 通过添加 columnDefs.targets 属性，使用从零开始的列索引来引用现有的列

如果我们添加了`columnDefs.targets`属性，我们应该确保数组从 0 开始计数时没有超出范围的索引。

例如，如果我们有下面的 HTML:

```
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js" integrity="sha512-894YE6QWD5I59HgZOGReFYm4dnWc1Qt5NtvYSaNcOP+u1T9qYdvdihz0PPSiiqn/+/3e7Jo4EaG7TubfWGUrMQ==" crossorigin="anonymous"></script>
<script src='//cdn.datatables.net/1.10.24/js/jquery.dataTables.min.js'></script>
<link rel='stylesheet' href='//cdn.datatables.net/1.10.24/css/jquery.dataTables.min.css'>
<table></table>
```

然后我们可以编写下面的 JavaScript 代码:

```
const dataSet = [
  ["Tiger Nixon", "System Architect", "Edinburgh", "5421", "2011/04/25", "$320,800"],
  ["Garrett Winters", "Accountant", "Tokyo", "8422", "2011/07/25", "$170,750"],
  ["Ashton Cox", "Junior Technical Author", "San Francisco", "1562", "2009/01/12", "$86,000"],
  ["Cedric Kelly", "Senior Javascript Developer", "Edinburgh", "6224", "2012/03/29", "$433,060"],
  ["Airi Satou", "Accountant", "Tokyo", "5407", "2008/11/28", "$162,700"],
  ["Brielle Williamson", "Integration Specialist", "New York", "4804", "2012/12/02", "$372,000"],
  ["Herrod Chandler", "Sales Assistant", "San Francisco", "9608", "2012/08/06", "$137,500"],
  ["Rhona Davidson", "Integration Specialist", "Tokyo", "6200", "2010/10/14", "$327,900"],
  ["Colleen Hurst", "Javascript Developer", "San Francisco", "2360", "2009/09/15", "$205,500"],
  ["Sonya Frost", "Software Engineer", "Edinburgh", "1667", "2008/12/13", "$103,600"],
  ["Jena Gaines", "Office Manager", "London", "3814", "2008/12/19", "$90,560"],
  ["Quinn Flynn", "Support Lead", "Edinburgh", "9497", "2013/03/03", "$342,000"],
  ["Charde Marshall", "Regional Director", "San Francisco", "6741", "2008/10/16", "$470,600"],
  ["Haley Kennedy", "Senior Marketing Designer", "London", "3597", "2012/12/18", "$313,500"],
  ["Tatyana Fitzpatrick", "Regional Director", "London", "1965", "2010/03/17", "$385,750"],
  ["Michael Silva", "Marketing Designer", "London", "1581", "2012/11/27", "$198,500"],
]jQuery('table').DataTable({
  data: dataSet,
  columns: [{
      title: "Name"
    },
    {
      title: "Position"
    },
    {
      title: "Office"
    },
    {
      title: "Extn."
    },
    {
      title: "Start date"
    },
    {
      title: "Salary"
    }
  ],
  columnDefs: [{
    orderable: false,
    targets: [0, 1, 2]
  }]
});
```

添加`columnDefs.targets`属性。

0 是第一列，1 是第二列，2 是第三列。

我们将`orderable`设置为`false`，因此我们禁止对这些列的项目进行重新排序。

# 结论

当我们试图添加一个包含 jQuery 数据表的表时，为了修复“无法读取未定义的属性样式”,我们应该确保`th`元素和`colspan`与列的数量相匹配。

此外，我们应该确保`columnDefs.targets`属性应该匹配表中列的索引。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)**和* [***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) ***。*****