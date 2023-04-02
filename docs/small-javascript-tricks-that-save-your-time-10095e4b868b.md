# 节省您时间的 JavaScript 小技巧

> 原文：<https://javascript.plainenglish.io/small-javascript-tricks-that-save-your-time-10095e4b868b?source=collection_archive---------17----------------------->

![](img/8c22d7fd3a32cb3480ad5ff3c8f2ff2a.png)

**这里有一个最简单的解决方案:**

```
<div class="part-content quiz">
  <h2>Chapter 1.1 End of Topic Quiz</h2>
   <p>
    The following quiz is meant to reinforce your understanding of the material presented above.
  </p>
  <!-- Question 1 Start -->
  <h4 class="quiz-question">1\. What is a statement? </h4>
  <button onclick="show_hide(this)" class="quiz-button">Show      Solution</button>
  <p id="answer">
   A <b>statement</b> is an instruction in a computer program that tells the computer to perform an action.
   </p>
   <br><br><hr>
   <!-- Question 1 End -->
<!-- Question 2 Start -->
  <h4 class="quiz-question">2\. What is a function? </h4>
   <button onclick="show_hide(this)" class="quiz-button">Show Solution</button>
<p id="answer">
A <b>function</b> is several statements that are executed sequentially.
</p>
<br><br><hr>

 </div>
```

在 Javascript 中:

```
<script>
         function show_hide(element)
         {
            var myAnswer = element.nextElementSibling; var displaySetting = myAnswer.style.display; var quizButton = element; if(displaySetting=="inline-block"){
                myAnswer.style.display = 'none'; quizButton.innerHTML = 'Show Answer';
            }
            else
            {
                myAnswer.style.display = 'inline-block';
                quizButton.innerHTML = 'Hide Answer';
            }
         }
</script>
```

有了这个，你就再也不需要参考答案的 ID 了。

onclick 属性中的“this”指的是按钮本身，“nextElementSibling”指的是下一个元素(它是

在您的情况下包含答案)。所以实际上`var myAnswer`的意思是获取按钮的下一个元素。

但是，使用这个函数，您需要确保按钮的下一个元素是答案元素，否则将不起作用。

同样，直接`var quizButton = document.getElementsByClassName('quiz-button');`不工作的原因是因为正如你所见，它得到多个元素 **s** 而不是一个元素。不同的元素可以有相同的类。这将返回具有类的元素的数组，而不是具有类的第一个元素。

*更多内容看* [***说白了就是 io***](http://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。*