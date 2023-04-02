# 去除 JavaScript 数组中重复值的 6 种非常有用的方法

> 原文：<https://javascript.plainenglish.io/6-extremely-useful-ways-to-remove-duplicate-values-in-javascript-arrays-b362f7b110b8?source=collection_archive---------7----------------------->

## 轻松实施阵列重复数据消除

![](img/7ef2abb337359a37dcfbbfc0c50e3df3.png)

Photo by [Alexandru Acea](https://unsplash.com/@alexacea?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

阵列重复数据消除是开发中经常遇到的热点问题。但是项目目前的情况是后端接口使用 SQL 去重，简单高效，基本不允许前端处理去重。

当然，这并不意味着前端重复数据删除是不必要的，仍然需要熟练使用。本文主要介绍几种常见的阵列去重方法，以增强对面试技巧的理解和掌握:)

# 1.索引 Of

使用`indexOf` 方法检测数组中第一个出现的元素是否等于该元素的当前位置。如果不相等，则意味着该元素是重复元素。

显然，对于重复元素，这两个位置是不同的。

# 2.分类

该方法首先调用数组的排序方法`sort()`，然后根据排序结果遍历比较相邻元素。如果它们相等，跳过改变元素，直到遍历结束。

这种排序方法解决了字符串出现在成员中的情况

# 3.ES6 地图

`Map` 是一种基于键值存储数据的结构，每个键只能对应一个唯一的值。并且映射的键会标识不同数据类型的数据，即 1 和“1”在映射中会被当作不同的键。

# 4.ES6 套件

ES6 中添加了数据类型集。set 最大的一个特点就是数据不重复。Set 函数可以接受数组(或类似数组的对象)作为参数进行初始化，此功能也可用于对数组进行重复数据消除

# 5.正常物体

利用对象键值的唯一性来达到效果

# 6.减少

利用`reduce`强大的上下文能力，第一个参数是函数，第二个参数会传递给第一个回调的 prev，返回值是下一次执行的 prev。

# 结论

阵列重复数据消除是开发中经常遇到的热点问题。我们可以根据不同的应用场景选择不同的实现方式，那么你喜欢哪一种，欢迎留言讨论。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*