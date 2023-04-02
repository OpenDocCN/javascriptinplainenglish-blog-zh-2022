# 使用 JavaScript 管理 HTML DOM 的更简单方法

> 原文：<https://javascript.plainenglish.io/an-easier-way-to-manage-html-dom-using-javascript-14e23a9cd4e1?source=collection_archive---------11----------------------->

## 为什么您应该将 HTML 代码生成方法作为最后的手段

![](img/66239e4375e70c843e4329e940cb3851.png)

Photo by [Hal Gatewood](https://unsplash.com/@halacious?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

我们雇佣新人，并在 [Freshbits](http://freshbits.in) 对他们进行内部培训。很多我们自己的学习发生在我们教他们基本知识的时候。

除此之外，我今天想分享的一个随机的[基本事情](https://blog.freshbits.in/the-correct-way-to-pass-methods-as-event-handlers-in-javascript)是关于使用 JavaScript 的 HTML 代码生成。

## **例句**

我们让初学者给他们用 JavaScript 构建的 HTML 页面添加一些交互性。可能是:

*   添加到电子商务页面上的购物车功能。
*   产品列表页面上的删除项目功能。
*   在结帐页面上添加地址功能等。

像 React、Vue 或 Angular 这样的 JavaScript 框架还不在他们的教学大纲中。他们使用 jQuery 或普通 JS 进行这类开发。

![](img/61796601452649eedcd90ded41e3a035.png)

有了手头的新机会和有限的工作经验，他们通常会兴奋地去争取，并想出如下的东西。

## **走老路💩**

我将以我们最新的团队成员 Utsav 完成的代码为例。他的任务是编写*添加到购物车*功能的代码。正如我们所料，他是这样编写功能的:

```
function displayCart() {
    // Abbreviating other stuff to focus on the core topic...

    for (let i = 0; i < cart.length; i++) {
        var imageTag = document.createElement('img');
        imageTag.src = cart[i].img;
        imageTag.setAttribute('class', 'w-10 h-10 object-cover rounded-md');
        document.getElementById('cart-item-' + i).appendChild(imageTag);

        var nameTag = document.createElement('span');
        nameTag.setAttribute('class', 'ml-4 font-semibold text-sm');
        nameTag.innerHTML = cart[i].name;
        document.getElementById('cart-item-' + id).appendChild(nameTag);

        var priceTag = document.createElement('div');
        priceTag.innerHTML = cart[i].price;
        document.getElementById('cart-item-' + id).appendChild(priceTag);

        var deleteTag = document.createElement('button');
        deleteTag.setAttribute('class', 'px-3 py-1 rounded-md bg-red-300 text-white');
        deleteTag.setAttribute('onclick', 'removeFromCart(' + cart[i].id + ')');
        deleteTag.innerHTML = "x";
        document.getElementById('cart-item-' + id).appendChild(deleteTag);

        // ...
    }
}
```

这种方法没有错。它只是**可读性和可维护性更差**。如果我们想在这个购物车中添加更多的元素呢？如果我们想改变风格呢？

有些人可能认为 jQuery 可以让它变得更好。虽然那些长长的代码行会更短，但主要问题仍然存在:*管理最终 HTML 输出的变化*

直接阅读和修改 HTML 更容易。让我们看看怎么做。

## **另一种方式🙅**

我们可以将相同的示例重写如下:

```
function displayCart() {
    // Abbreviating other stuff to focus on the core topic...

    for (let i = 0; i < cart.length; i++) {
        var cartItemHtml = [
            '<div id="cart-item-' + i + '">',
                '<img class="w-10 h-10 object-cover rounded-md" src="' + cart[i].img + '" />',
                '<span class="ml-4 font-semibold text-sm">' + cart[i].name + '</span>',
                '<div>' + cart[i].price + '</div>',
                '<button class="px-3 py-1 rounded-md bg-red-300 text-white" onclick="removeFromCart(' + cart[i].id + ')">x</button>',
            '</div>'
        ].join("\n");

        // ...
    }
}
```

现在有了更好的可读性。我们可以看到最终的 HTML 会是什么样子。但是，HTML 代码被合并到 JavaScript 中，所以我们不得不经常使用这些引用。更进一步是使 HTML 代码独立。

## **更好的办法🤗**

有一个[模板](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/template) HTML 标签默认不显示在页面上。我们可以用它来托管我们的 HTML 代码，比如:

```
<template id="cart-item">
    <div>
        <img class="w-10 h-10 object-cover rounded-md cart-item-image" />
        <span class="ml-4 font-semibold text-sm cart-item-name"></span>
        <div class="cart-item-price"></div>
        <button class="px-3 py-1 rounded-md bg-red-300 text-white cart-item-delete">x</button>
    </div>
</template>
```

看起来代码很容易维护，对吗？现在我们如何在你问的 JavaScript 中使用它？

```
function displayCart() {
    // Abbreviating other stuff to focus on the core topic... var template = document.getElementById('cart-item');for (let i = 0; i < cart.length; i++) {
        var cartItemTag = template.content.cloneNode(true);

        cartItemTag.querySelector("img.cart-item-image").src = cart[i].img; 
        cartItemTag.querySelector("span.cart-item-name").innerHTML = cart[i].name;
        cartItemTag.querySelector("div.cart-item-price").innerHTML = cart[i].price;
        cartItemTag.querySelector("button.cart-item-delete").onclick = function() { removeFromCart(cart[i].id) };
    }
}
```

这样，我们的 JavaScript 可以直接针对模板内的每个元素，分别设置属性和内容。

有什么方法可以更进一步吗？如果你有任何想法，请分享。

## **上发条**

这种学习主要是针对初学 HTML 和 JavaScript 的初学者。随着他们的发展，有更多的选择，比如使用[模板引擎](https://colorlib.com/wp/top-templating-engines-for-javascript)或者使用成熟的 [JS 框架](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks)，在那里你管理数据，框架通过反应性来处理 DOM 更新。

就是这样。如果您有一些生成 HTML 的 JS 代码，今天就尝试一下模板标签，让我们知道它的进展如何。另一边见。

*原发布于*[*https://blog . fresh bits . in*](https://blog.freshbits.in/an-easier-way-to-manage-html-dom-using-javascript)*。*

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。***