# SQL 联接类型(用图像描述)

> 原文：<https://javascript.plainenglish.io/what-are-sql-join-types-described-with-image-281c10949818?source=collection_archive---------17----------------------->

## 通过理解连接类型的基础知识，有效地使用 SQL

![](img/6f54804c7733028af9a776f18d260f58.png)

Two Full Outer Joins

Join 是 SQL servers 中使用最广泛的子句。join 子句用于从两个或多个表中检索和组合数据。今天，我们将讨论用图片描述的 SQL 连接类型。

所以我们开始吧！

## 示例模式

为了便于理解，我们假设有三个表。下面是一些表格

**表 1**

![](img/e86a40a69276f7707e152a568a2fcde8.png)

Table 1

**表二**

![](img/ad02927018d0ec59c1b68a127357bd22.png)

Table 2

**表 3**

![](img/d5d01e905f4634ea434dc61543b8783f.png)

Table 3

# 让我们开始描述 SQL 连接类型

## 从两个表中选择

![](img/ad32a2b19ec66deab4f06bdfe48a35d9.png)

Two Tables

```
SELECT *
FROM Table1;SELECT *
FROM Table2;
```

## 左外部连接

![](img/dfb461269aecb4a11254c550bbcbe2f8.png)

Left Outer Join

```
SELECT *
FROM Table1 t1
LEFT OUTER JOIN Table2 t2
ON t1.fk = t2.id;
```

## 半连接

![](img/5eb38d0dba711ebab36a6586a5b90e77.png)

Semi Join

```
SELECT *
FROM Table1 t1
WHERE EXISTS (SELECT 1FROM Table2 t2
WHERE t1.fk = t2.id
);
```

## 排除的左外连接

![](img/6fbdd068381dc20e117ab55ebe16e49b.png)

Left Outer Join with exclusion

```
SELECT *
FROM Table1 t1
LEFT OUTER JOIN Table2 t2
ON t1.fk = t2.id
WHERE t2.id IS NULL;
```

## 完全外部连接

![](img/7f43e51f56c9e247f08e0d3b8b19e6ef.png)

Full Outer Join

## 排除的完全外部连接

![](img/77ad7fdce0740b9ee4a3a20d5d0108d1.png)

FULL OUTER JOIN with exclusion

```
SELECT *
FROM Table1 t1
FULL OUTER JOIN Table2 t2
ON t1.fk = t2.id
WHERE t1.fk IS NULL
OR t2.id IS NULL;
```

## 内部连接

![](img/5eb38d0dba711ebab36a6586a5b90e77.png)

Inner Join

```
SELECT *
FROM Table1 t1
INNER JOIN Table2 t2
ON t1.fk = t2.id;
```

## 右外部联接

![](img/5edab62028733c8a2ce637595ab35db5.png)

Right Outer Join

```
SELECT *
FROM Table1 t1
RIGHT OUTER JOIN Table2 t2
ON t1.fk = t2.id;
```

## 反半连接

![](img/f504f222555d3aac74c8e96c4e93ff9f.png)

Anti Semi Join

```
SELECT *
FROM Table1 t1
WHERE NOT EXISTS (SELECT 1FROM Table2 t2
WHERE t1.fk = t2.id
);
```

## 排除的右外连接

![](img/a2e540e04d50d4174caebaddc72db1e3.png)

Right Outer Join with Exclusion

```
SELECT *
FROM Table1 t1
RIGHT OUTER JOIN Table2 t2
ON t1.fk = t2.id
WHERE t1.fk IS NULL;
```

## 交叉连接-笛卡尔乘积

![](img/f11116b45701b499c00ffe7eec419268.png)

CROSS JOIN- the Cartesian product

```
SELECT *
FROM Table1 t1
CROSS JOIN Table2 t2;
```

## 非对等内部连接

![](img/5eb38d0dba711ebab36a6586a5b90e77.png)

NON-EQUI INNER JOIN

```
SELECT *
FROM Table1 t1
INNER JOIN Table2 t2
ON t1.fk >= t2.id;
```

## 交叉应用

![](img/6eb0f2d1edc95a9a56edea639b0bc9af.png)

Cross Apply

```
SELECT *
FROM Table1 t1
CROSS APPLY[dbo].[someTVF](t1.fk)
AS t;
```

## 外部应用

![](img/eb15594600a4b42074b8af3b3f9469ba.png)

Outer Apply

```
SELECT *
FROM Table1 t1
OUTER APPLY[dbo].[someTVF](t1.fk)
AS t;
```

## 两个完整的外部连接

![](img/6f54804c7733028af9a776f18d260f58.png)

Two Full Outer Joins

```
SELECT *
FROM Table1 t1
FULL OUTER JOIN Table2 t2
ON t1.fk = t2.id
FULL OUTER JOIN Table3 t3
ON t1.fk_table3 = t3.id;
```

## 两个内部连接

![](img/539b650e951f0fad029f3de86adda926.png)

Two Inner Joins

```
SELECT *
FROM Table1 t1
INNER JOIN Table2 t2
ON t1.fk = t2.id
INNER JOIN Table3 t3
ON t1.fk_table3 = t3.id;
```

## 两个左外部连接

![](img/b356c4316d964682d436056a922d5624.png)

Two Left Outer Joins

```
SELECT *
FROM Table1 t1
LEFT OUTER JOIN Table2 t2
ON t1.fk = t2.id
LEFT OUTER JOIN Table3 t3
ON t1.fk_table3 = t3.id;
```

## 内部连接和左外部连接

![](img/2c15c3b356d971ddb42ad5e7fb6a6e7b.png)

INNER JOIN and a LEFT OUTER JOIN

```
SELECT *
FROM Table1 t1
INNER JOIN Table2 t2
ON t1.fk = t2.id
LEFT OUTER JOIN Table3 t3
ON t1.fk_table3 = t3.id;
```

## 除...之外

![](img/95b9aab94bb392a0c8e3002b21c66201.png)

Except

```
SELECT fk as id
FROM Table1
EXCEPT
SELECT ID
```

## 联盟

![](img/f11116b45701b499c00ffe7eec419268.png)

Union

```
SELECT fk as id
FROM Table1
UNION
SELECT ID
```

## 横断

![](img/25d47ec8ff06cfc714b813bc2dc734bf.png)

Intersect

```
SELECT fk as id
FROM Table1
INTERSECT
SELECT IDFROM Table2:
```

## 最后的想法

![](img/1aa1dd96788d659b2ac6224d1d8709c4.png)

Photo by [Jens Lelie](https://unsplash.com/@madebyjens?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

希望你喜欢这篇文章，它会对你有所帮助。

编程快乐！:D

***这是我的另一篇关于 SQL cheatsheet 的文章。希望对你们也有帮助。***

[](https://blog.devgenius.io/sql-cheatsheet-you-will-find-useful-b5316f308525) [## 你会发现有用的 SQL Cheatsheet

### 使用此备忘单，让您的 SQL 之旅更加轻松

blog.devgenius.io](https://blog.devgenius.io/sql-cheatsheet-you-will-find-useful-b5316f308525) 

*更多内容请看**[***说白了. io***](https://plainenglish.io/) *。报名参加我们的**[***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们* [***推特***](https://twitter.com/inPlainEngHQ) *和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。***