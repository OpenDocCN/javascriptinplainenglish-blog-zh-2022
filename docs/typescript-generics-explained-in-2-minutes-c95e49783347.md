# 用 2 分钟的时间用例子解释了类型脚本泛型

> 原文：<https://javascript.plainenglish.io/typescript-generics-explained-in-2-minutes-c95e49783347?source=collection_archive---------6----------------------->

## 深入探究类型脚本泛型

![](img/9454c2598a5453234177f4a92a8d17d3.png)

TypeScript 是强大的，它可以使您的代码更加稳定、易读、易于重构等等。

TypeScript 包含 ***泛型*** ，这在想要编写干净的可重用代码时非常有用。 ***泛型*** 为开发人员提供了一种创建可重用代码的方式，它的工作方式使得组件可以与任何数据类型一起工作，而不局限于单一数据类型。

鉴于您已经阅读了这篇文章，我希望您已经了解了 TypeScript 的基础知识，并且希望了解更多关于 TypeScript 中的 ***泛型*** 的知识，所以我不会深入解释 TypeScript 本身。

考虑以下代码:

```
let courses = [];const fetchCourseTemplates = async () => {
  isLoading = true;
  const companyId = '123';
  try {
    courses = await getAllDocuments(`course_templates/${companyId}/templates`);
    isLoading = false;
  } catch (e) {
    isLoading = false;
    throw new ***Error***('Cant load templates: ' + e);
  }
};
```

我们调用的函数将如下所示:

```
// Our reuseable function to get data
export const getAllDocuments = async (collectionName: string) => {
  const documents = [];
  const querySnapshot = await getDocs(collection(db, collectionName));
  querySnapshot.forEach((doc) => {
    const data = doc.data();
    documents.push({
      id: doc.id,
      ...data
    });
  });

  return documents;
};
```

在上面的代码中，您从一个 API 获取一些数据，并传递一个关于在哪里获取数据的参数(在本例中，是对 Firebase 中一个集合的引用)。从函数传回的数据存储在一个变量中。一切都好，对吧？

不完全是。你看，如果你有一个可重用的函数从集合中获取数据，你永远不知道你实际上得到的是哪种类型的数据。你现在可能知道了，但 TypeScript 不知道。

假设您正在使用这个函数从 Firebase 的不同地方检索各种不同的文档，您得到的数据很可能会不时地有所不同。那么我们如何让 TypeScript 开心呢？

# 介绍泛型

在这种情况下，泛型将帮助您。您可以扩展该函数以使用泛型，并且在调用该函数时，您可以指定正在处理的数据类型。这样会让 TypeScript 看得懂。

让我们看看上面的代码，看看使用泛型会是什么样子。

```
let courses: Course[] = [];const fetchCourseTemplates = async () => {
  isLoading = true;
  const companyId = '123';
  try {
    courses = await getAllDocuments<Course>(`course_templates/${companyId}/templates`);
    isLoading = false;
  } catch (e) {
    isLoading = false;
    throw new ***Error***('Cant load templates: ' + e);
  }
};
```

这里的主要区别在于等待。你可能会注意到<course>。这基本上就是我向函数传递一个类型，告诉 TypeScript 函数应该处理什么数据。让我们看看下一个函数</course>

```
// Our reuseable function to get data
export const getAllDocuments = async <T>(collectionName: string) => {
  const documents: T[] = [];
  const querySnapshot = await getDocs(collection(db, collectionName));
  querySnapshot.forEach((doc) => {
    const data = doc.data();
    documents.push({
      ...data
    } as T);
  });

  return documents;
};
```

注意 async 关键字后，我做 ***< T >*** 。这是我把调用函数的类型取回来。再往下，你会看到我创建的数组应该是我传递的类型(我们通过了**课程**)。当我们返回时，TypeScript 现在知道我正在返回我提供的任何类型。在我们的例子中，它将返回一个课程数组，因为我们在***fetchcoursetypes***函数中将课程作为我们的类型传递。

差不多结束了！我希望你理解了以上内容。当然，除了我刚才展示的，还有更多关于泛型的东西和用例，但希望它能给你一个基本的理解，你能明白它为什么强大。

***如果你想找个时间和我聊聊，请关注我的***[***Twitter***](https://twitter.com/nickycdk)***|***[***LinkedIn***](https://www.linkedin.com/in/dknickychristensen/)***或者直接访问我的*** [***网站***](https://nickychristensen.dk/) ***(丹麦文)***

**更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *中获得独家写作机会和建议。**