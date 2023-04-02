# 每个 JavaScript 程序员必须知道的 5 个概念

> 原文：<https://javascript.plainenglish.io/5-concepts-every-javascript-programmer-must-know-6a5f6df325ce?source=collection_archive---------4----------------------->

## 这里是 JavaScript 开发人员必须知道的 5 个概念。

![](img/b80c1f7277207dabfedac1f451185663.png)

Photo by [Andrea Piacquadio](https://www.pexels.com/photo/woman-in-white-long-sleeve-shirt-using-silver-laptop-computer-3784324/)

JavaScript 是让互联网工作的编程语言。没有 JavaScript，互联网将一无是处。在这篇文章中，我介绍了每个 JavaScript 程序员都必须知道的一些 JavaScript 基本概念。

# 1.异步等待:

Async & Await 让承诺更容易书写。

在 JavaScript 中，异步模式可以在各种版本中处理，

*在 ES5 中，通过“回调”*来完成

*在 ES6 中，这是由“承诺”完成的*

*在 ES7 中，由“异步&等待”*完成

但是很多人对 async & await 的基础有误解。异步/等待仅基于承诺。每个*异步*函数都返回一个承诺。await 关键字只能在一个异步函数中使用，你将*等待的一切，*将是一个承诺。

```
async function dets() {
   try {
      let var=await users();
      return var[0].user;
   } catch (err) {
       return {
          user: ‘default user’
       };
   }
}
```

要了解 Async & Await，首先需要正确理解承诺。如果你能理解 async & await，这将有助于你轻松实现函数式编程，并增加代码的可读性。

# 2.理解承诺

一个承诺是一个异步函数的结果。Promise 对象表示异步操作的最终完成(或失败)及其结果值。承诺可以用来避免连锁回调。

承诺处于以下状态之一:

*   *待定*:初始状态，未完成也未拒绝。
*   *完成*:表示操作成功完成。
*   *拒绝*:表示操作失败。

将这段代码视为异步执行数据库操作的示例承诺。

```
var p1 = new Promise(function(resolve, reject) {
    opCompleted = false;
    if (opCompleted) {
        resolve('Done');
    } else {
        reject('Not Done');
    }
});
p1.then(function(result) {
    console.log(result);         //Output : Done
}).catch(function(error) {
    console.log(error);         //if opCompleted=FALSE                                                  
                                //Output : Not Done
})
```

# 3.JavaScript 中的多态性

多态性是面向对象编程的核心之一。简而言之，我们可以将多态性定义为一个消息以多种形式显示的能力。它是设计对象来共享行为并能够用特定的行为覆盖共享行为的实践。多态利用继承来实现这一点。

JavaScript 中覆盖函数的例子—

```
var p = new People('raja');//override function People.prototype.getDetails = function() {
    return this.name.toUpperCase();
}console.log(p.getDetails());         //outPut: RAJA//object and prototype function
function People(name) {
    this.name = name;
}People.prototype.getDetails = function() {
    return this.name;
}
```

在上述基于原型的程序方法中，构造函数必须被另一个原型函数覆盖，以大写形式返回名称。

所以我们可以在不同的作用域中重写一个函数，方法重载也是可能的。JS 没有重载 native 的方法，但是我们仍然可以实现它。

# 4.Currying

它是一种将多参数函数转化为序列中几个单参数函数的方法。

简而言之，函数不是一次接受一个参数，而是接受第一个参数并返回一个接受第二个参数的新函数，然后返回一个接受第三个参数的新函数，这个过程一直持续到所有参数都满足为止。

示例:

```
var add = function (a){
   return function(b){
      return function(c){
         return a+b+c;
      }
   }
}console.log(add(5)(6)(7));        //output 18
```

Currying 有助于创建高阶函数，在事件处理中非常方便。

# 5.提升

JS 中的提升是一种机制，在代码执行之前，函数和变量声明被移动到它们作用域的顶部。提升允许在声明函数之前在代码中安全地使用函数。

让我们用一个例子来理解-

```
console.log(Hoist);
var Hoist = ’The variable Has been hoisted’;
//output : undefined//
```

这里，JavaScript 挂起了变量声明。这就是解释器所看到的上面的代码，

```
var Hoist;
console.log(Hoist);
Hoist = ’The variable Has been hoisted’;
```

JavaScript 只提升声明，不提升初始化。这意味着无论在哪里声明函数和变量，无论它们的作用域是全局的还是局部的，它们都被移动到作用域的顶部。

如需了解更多信息，请参考本网站[](https://scotch.io/tutorials/understanding-hoisting-in-javascript)

# *最后的想法*

*这里是我认为每个 JavaScript 程序员都必须知道的 5 个 JavaScript 概念。这将有助于你事业的发展。*

*我希望这篇文章对你有所帮助，并让你学到一些新东西。与你的网络开发者朋友分享这篇精彩的文章😀。我将很快就这个话题写更多的文章。*

**在我的下一篇文章中再见…**

*![](img/c943b71411d6fb4cd3c304083a8f516d.png)*

*GIF From [GIPHY](https://media.giphy.com/media/YorwDAH66ln3O/giphy.gif)*

**更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) *，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***