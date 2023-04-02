# 使用可排序的 Js 库拖放

> 原文：<https://javascript.plainenglish.io/drag-drop-with-sortable-js-library-154627f467b3?source=collection_archive---------13----------------------->

在 JavaScript 中，拖放功能允许用户单击一个元素并将其拖到不同的位置，或者放到另一个元素上。例如，这对于允许用户重新排列列表中的项目或者创建交互式图形是很有用的。

要在 JavaScript 中实现拖放，可以使用 HTML5 拖放 API。该 API 提供了一组事件和相关方法，允许您向网页添加拖放功能。

下面是如何使用 HTML5 拖放 API 在 JavaScript 中实现拖放的简单示例:

![](img/63dbd3191610a15e2744df058ba0a98a.png)

可排序的 JavaScript 库，用于向 ID 为“drop-items”的元素添加拖放功能。Sortable 库使创建可排序列表和网格变得容易，并提供了一个简单的 API，用于向 web 页面上的元素添加拖放行为。

该代码通过传入可排序的元素(`dropItems`)和一个 options 对象来创建一个新的可排序实例。options 对象为 Sortable 实例指定了一些配置选项，例如动画持续时间(`animation`)和应用于被拖动元素(`dragClass`)和被选择元素(`chosenClass`)的 CSS 类。

使用这段代码，用户将能够单击“drop-items”元素中的一个元素，并将其拖动到元素中的不同位置。元素将根据它们的新位置重新排序，而 chosen 和 drag CSS 类将根据需要应用于元素。

要在 HTML、CSS 和 JavaScript 中实现拖放，可以使用 HTML5 拖放 API。以下是在网页中实现拖放的分步指南:

1.  创建可拖动的 HTML 元素。使元素可拖动。例如，我们定义了类。滴

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Drag and Drop Card</title>
    <link rel="stylesheet" href="./style.css" />
  </head>
  <body>
    <div class="drop">
      <div class="drop_container" id="drop-items">
        <div class="drop_card">
          <div class="drop_data">
            <img src="http://shorturl.at/sWY25"
            alt="img1"
            class="drop_img"
            />
            <div>
              <h1 class="drop_name">Zealy</h1>
              <span class="drop_profession">Data Engineer</span>
            </div>
          </div>
          <div>
            <a href="#" class="drop_social"><i class="bx bxl-instagram"></i></a>
            <a href="#" class="drop_social"><i class="bx bxl-facebook"></i></a>
            <a href="#" class="drop_social"><i class="bx bxl-twitter"></i></a>
          </div>
        </div>
        <div class="drop_card">
          <div class="drop_data">
            <img src="http://shorturl.at/kmwZ3"
            alt="img1"
            class="drop_img"
            />
            <div>
              <h1 class="drop_name">Domey</h1>
              <span class="drop_profession">Software Engineer</span>
            </div>
          </div>
          <div>
            <a href="#" class="drop_social"><i class="bx bxl-instagram"></i></a>
            <a href="#" class="drop_social"><i class="bx bxl-facebook"></i></a>
            <a href="#" class="drop_social"><i class="bx bxl-twitter"></i></a>
          </div>
        </div>
        <div class="drop_card">
          <div class="drop_data">
            <img src="http://shorturl.at/agFY7"
            alt="img1"
            class="drop_img"
            />
            <div>
              <h1 class="drop_name">Greeney</h1>
              <span class="drop_profession">Product Marketing</span>
            </div>
          </div>
          <div>
            <a href="#" class="drop_social"><i class="bx bxl-instagram"></i></a>
            <a href="#" class="drop_social"><i class="bx bxl-facebook"></i></a>
            <a href="#" class="drop_social"><i class="bx bxl-twitter"></i></a>
          </div>
        </div>
        <div class="drop_card">
          <div class="drop_data">
            <img src="http://shorturl.at/sxDMU"
            alt="img1"
            class="drop_img"
            />
            <div>
              <h1 class="drop_name">Benny</h1>
              <span class="drop_profession">UX Writer</span>
            </div>
          </div>
          <div>
            <a href="#" class="drop_social"><i class="bx bxl-instagram"></i></a>
            <a href="#" class="drop_social"><i class="bx bxl-facebook"></i></a>
            <a href="#" class="drop_social"><i class="bx bxl-twitter"></i></a>
          </div>
        </div>
      </div>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/sortablejs@latest/Sortable.min.js"></script>
    <script src="./script.js"></script>
  </body>
  </html>
```

2.添加要应用于可拖动元素的 CSS 样式。例如:

```
:root {
  --first-color: #272a3a;
  --first-color-light: #8a8eaa;
  --first-color-lighten: #f8f8fc;
  --body-font: "Ubuntu", sans-serif;
  --normal-font-size: 1rem;
  --smaller-font-size: 0.813rem;
}
*,
::before,
::after {
  box-sizing: border-box;
}
body {
  margin: 0;
  padding: 0;
  font-family: var(--body-font);
  background-color: var(--first-color-lighten);
}
h1 {
  margin: 0;
}
a {
  text-decoration: none;
}
img {
  max-width: 100%;
  height: auto;
}
.drop,
.drop_container {
  display: grid;
}
.drop {
  height: 100vh;
  align-items: center;
  justify-content: center;
}
.drop_container {
  row-gap: 1rem;
  padding: 2rem;
  box-shadow: 4px 4px 16px #e1e1e1;
}
.drop_card,
.drop_data {
  display: flex;
  align-items: center;
}
.drop_card {
  width: 360px;
  justify-content: space-between;
  padding: 0.75rem 1.25rem.75rem 0.75rem;
  background-color: var(--first-color-lighten);
  box-shadow: 4px 4px 16px #e1e1e1, -2px -2px 16px #fff;
  border-radius: 2.5rem;
}
.drop_img {
  width: 55px;
  height: 55px;
  border-radius: 50%;
  margin-right: 1rem;
}
.drop_name {
  font-size: var(--normal-font-size);
  color: var(--first-color);
  font-weight: 500;
}
.drop_profession {
  font-size: var(--smaller-font-size);
  color: var(--first-color-light);
}
.drop_social {
  margin: 0 0.375rem;
  color: var(--first-color-light);
  transition: 0.4s;
}
.drop_social:hover {
  color: var(--first-color);
}
.sortable-chosen {
  box-shadow: 8px 8px 32px #e1e1e1;
}
.sortable-drag {
  opacity: 0;
}
```

3.添加 JavaScript 代码来处理拖放事件。以下是如何处理这些事件的示例:

```
const dropItems = document.getElementById('drop-items')
new Sortable(dropItems, {
  animation: 350,
  chosenClass: "sortable-chosen",
  dragClass: "sortable-drag"
});
```

通过这些步骤，您可以向 web 页面添加拖放功能，允许用户根据需要移动和重新排列元素。

源代码:【https://github.com/easywebsify/drag-and-drop 

## 更多内容请访问 [PlainEnglish.io](https://plainenglish.io/) 。

*报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们上* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *

## *希望扩大你的科技创业公司的知名度和采用率吗？检查[电路](https://circuit.ooo/?utm=publication-post-cta)。*