# 解释 Cookies:数据存储

> 原文：<https://javascript.plainenglish.io/explaining-cookies-data-storage-a2c194ad3e7?source=collection_archive---------9----------------------->

## 什么是 cookies，如何使用它们，以及如何管理它们。

![](img/35790d9451e17d5a3dd9838a0cb18c3c.png)

Photo by [Kaleidico](https://unsplash.com/@kaleidico?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Cookies 是一种存储在 web 浏览器中的数据。它们用于存储您与网站的交互信息，并可用于改善您在网站上的用户体验。在这篇博文中，我们将讨论什么是 cookies，如何使用它们，以及如何管理它们。

## 什么是饼干？

cookie 是存储在您的计算机或移动设备上的一小段数据。当您访问网站时，该网站可能会向您的浏览器发送 cookie。然后，您的浏览器可能会将 cookie 存储在您的计算机或移动设备上。cookie 是网站用来记住你的偏好和活动的一小段信息。

## 饼干是怎么用的？

Cookies 有多种用途，例如让您登录到自己的帐户、记住您的偏好以及提供个性化内容。cookies 的一个常见用例是存储用户的会话 ID。当您登录网站时，该网站可能会向您的浏览器发送一个包含会话 ID 的 cookie。当您在网站上从一个页面移动到另一个页面时，会话 ID 用于识别您的身份。

您可以通过更改浏览器设置来管理您的 cookies。大多数浏览器允许您查看、删除和控制 cookies。您也可以设置您的浏览器阻止所有 cookies。但是，阻止 cookies 可能会阻止您使用网站上的某些功能。

## 如何用 JavaScript 创建 Cookie

您可以使用`document.cookie`属性在 JavaScript 中创建一个 cookie。`document.cookie`属性是一个字符串，包含 cookie 的名称、值和到期日期。名称和值由等号(=)分隔。截止日期是可选的，以 GMT 格式指定。如果不指定过期日期，cookie 将在浏览器关闭时过期。

要创建 cookie，您必须首先指定 cookie 的名称和值。名称用于标识 cookie，值用于存储用户信息。例如，您可以创建一个名为“user”的 cookie，其值为“John Doe”。

```
document.cookie = “user=John Doe”;
```

接下来，您必须指定 cookie 的到期日期。截止日期是可选的，以 GMT 格式指定。如果不指定过期日期，cookie 将在浏览器关闭时过期。您可以使用 expires 属性来设置 cookie 的到期日期。

以下代码将 cookie 的到期日期设置为 2025 年 1 月 1 日。

```
document.cookie = “user=John Doe; expires=Thu, 01 Jan 2025 00:00:00 GMT”;
```

您还可以使用 max-age 属性来设置 cookie 的到期日期。max-age 属性以秒为单位指定。以下代码将 cookie 的到期日期设置为一分钟。

```
document.cookie = “user=John Doe; max-age=60”;
```

![](img/8ca0de9ab783f285f3f2653f74a2f509.png)

Photo by [Kiyun Lee](https://unsplash.com/@kiyun911?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 在 JavaScript 中删除 Cookie

您可以通过将 cookie 的到期日期设置为过去的日期来删除 JavaScript 中的 cookie。以下代码将 cookie 的到期日期设置为 1970 年 1 月 1 日。

```
document.cookie = “user=John Doe; expires=Thu, 01 Jan 1970 00:00:00 GMT”;
```

您也可以使用最大年龄属性来删除 cookie。以秒为单位指定最大年龄属性。下面的代码将 cookie 的过期日期设置为-60。

```
document.cookie = “user=John Doe; max-age=-60”;
```

## 结论

在这篇博客文章中，我们讨论了什么是 cookies，它们是如何使用的，以及您如何管理它们。我们还展示了如何在 JavaScript 中创建和删除 cookies。Cookies 是存储用户信息的有用工具。

我希望这篇文章能澄清你的困惑！祝你的编码项目好运！