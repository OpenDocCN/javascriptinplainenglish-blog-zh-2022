# 如何使用 JavaScript 承诺或 TypeScript 承诺

> 原文：<https://javascript.plainenglish.io/how-to-use-javascript-promises-or-typescript-promises-538330eb0788?source=collection_archive---------14----------------------->

## 关于如何处理 JavaScript 承诺和 TypeScript 承诺的简单解释。

当我们需要的数据不能立即得到时，JavaScript 的承诺是很重要的。在本文中，我们将使用一个简单的 John 和 Jane 生日约定。

![](img/1bf05c39970ea97a38a900ee4618ee2d.png)

How to use JavaScript promises or Typescript promises

好吧，说实话，在这个时代，**时间**往往是至关重要的，我们都必须同意这一点。但这并不意味着我们不能找到**可选地**与之绑定的方法。我们可以选择**等待**或**从我们停止的地方**继续，这两个概念是我们今天主题的基础，JavaScript 承诺。

所以，在我看来，最好的学习方法是与现实世界进行类比。因此，我们将使用一个简单的例子，以便我们了解 JavaScript 承诺是什么，以及实际上如何使用它们。

由于 TypeScript 是 JavaScript 的超集，因此可以应用相同的规则。因此，在处理 TypeScript 承诺时，可以应用相同的逻辑。

**示例案例**

嗯，约翰和简是多年的朋友，在他们的任何一个生日，他们都同意奖励生日主人去保龄球馆。所以，这是一个**小拇指的承诺**他们做出了，并且必须在他们的余生中遵守。

嗯，今年是简的生日，由于某些原因，约翰的薪水延迟了，不能像预期的那样按时发放，所以他给了简两个选择:

1.  她可以等到月底约翰发工资，他们去打保龄球。
2.  约翰一有钱，就会带她去打保龄球。

嗯，我不知道你会选择哪一个，但在我看来，你会选择最适合你的那个。

**用 JavaScript 解释承诺**

因此，在上面的简单类比中，我们将使用几个关键字来清晰地展现 JavaScript 的承诺。这些是:

1.  生日所有者——但是我们将使用 Jane，因为在这种情况下她是所有者。
2.  小指承诺。
3.  准时。
4.  等待直到**月底**。
5.  一旦。

因此，让我们开始打破每个部分，看看什么是引擎盖下！

**代码设置**

这是这个类比的完整代码。我们将用它来解释如何使用 JavaScript promises，所以你可以根据需要参考这个。

```
/**
 * A pact between John and Jane, old time friends.
 * 
 * NOTE: Some of the concepts such as resolving JavaScript Promises
 * are not explained here.
 */
class JohnAndJanePact {
    /**
     * The agreed bowling voucher ticket value, irrespective of
     * any delays.
     */
    bowlingTicketVoucherValue = 1000;constructor() {
        this.makeClaim();
    }/**
     * The birthday owner is the one who is charged with the role of
     * making the claim for their gift.
     */
    makeClaim() {

        // Using patientjane
        this.patientJane();// To use eagerJane, simply uncomment the below line
        // this.eagerJane();
    }/**
     * She is the patient version of Jane the birthday owner.
     * 
     * You will notice that patientJane's social life will be blocked until
     * john fulfills his bowling gift voucher to her.
     */
    async patientJane() {
        const voucher = await this.endMonthJohn();
        console.log(`End Month Salary Was Paid So John Sent Voucher -> ${voucher}`)
        this.socialLifeOfJane();
    }/**
     * She is the eager version of Jane the birthday owner.
     * 
     * You will notice that eagerJane's social life will keep on rolling!
     */
    eagerJane() {
        this.sideIncomeJohn().then(voucher => {
            console.log(`Side Income Came So John Sent Voucher -> ${voucher}`)
        });
        this.socialLifeOfJane();
    }/**
     * The rest of her social life.
     */
    socialLifeOfJane() {
        console.log(`Jane's social life...`)
    }/**
     * This john will wait for the end of the month to be paid.
     */
    async endMonthJohn() {
        return this.waitForSalary();
    }/**
     * Simulate john waiting for his salary to be available.
     * 
     * We are using 3000 as the default timeout to mock a salary
     * at the end of the month, you are free to change this value.
     */
    async waitForSalary() {
        return new Promise((resolve, reject) => {
            setTimeout(() => {
                resolve(this.bowlingTicketVoucherValue)
            }, 3000);
        })
    }/**
     * This john has a side income, so they will provide the
     * voucher as soon as one of their side incomes generate a profite
     */
    async sideIncomeJohn() {
        return this.waitForEarlySideIncome();
    }/**
     * Simulate john waiting for his early side income salary to be available.
     * 
     * We are using a default timeout of 1000 to mock an early side income, feel
     * free to change this value as well.
     */
    async waitForEarlySideIncome() {
        return new Promise((resolve, reject) => {
            setTimeout(() => {
                resolve(this.bowlingTicketVoucherValue)
            }, 1000);
        })
    }
}// instantiate the pact
new JohnAndJanePact();
```

**生日主人**

因此，我们可以把 Jane 看作是我们程序/代码的一部分，它需要来自另一部分(John)的数据。现在，简，作为一个函数，可以像往常一样继续她的社交生活，或者，如果绝对必要的话，**她必须等待约翰完成他的交易。**

**小指承诺**

因为约翰和简被一个小手指的承诺所束缚，我们都知道，你永远不会违背小手指的承诺，那么约翰必须确保无论如何，他需要交付。因此，约翰将被**绑定**到承诺上，而**简将等待**承诺被**解决**。

现在，如果你从 JavaScript 承诺的角度考虑，它以类似的方式工作。必须有一方**提供**承诺，另一方**消费**承诺。

通过将 john 的**变体标记为 **async** ，这隐含地使它们默认返回一个承诺。**

另一件要注意的事情是，我们将**病人简**标记为**异步**，以便她能够**等待**承诺被解决。

**按时**

所以，既然约翰不能按时完成他的交易，那么在这种情况下，他必须给简我们上面提到的选择。

类似地，这同样适用于使用 JavaScript。程序的一部分可以立即返回需要的数据**和**总是按照预期的**而没有延迟，**或**它可以**去获取提供给它的数据**。**

**这就是 JavaScript 的前景，这就是我们对 JavaScript 前景的真实定义:**

**你的程序的一部分在将来的某个时间点向它们的调用者提供数据的承诺。**

**所以，这基本上是我对 JavaScript 承诺的现实定义。因此，为了进一步理解这一点，让我们通过理解我们上面列出的最后两个关键字(4 和 5)来关注术语 ***未来时间点*** 。**

****等到月底****

**所以，简可以选择等到月底再给约翰发工资。这意味着她所有的社交生活都将暂停，直到约翰的保龄球债务还清。**

**因此，这引入了 JavaScript 承诺的概念，称为 **async-await** 。嗯，如你所见，我们有 **await，有点类似于 wait** 。所以，这将意味着简、**将等到约翰拿到钱**，那将是在月末**。****

****类似地，当您使用 async — await 选项时，这意味着需要的数据将在一段时间后才可用。一旦数据可用，就可以使用了。****

****这里我们将使用 **patientJane** 来等待 **endMonthJohn** 。此外，如上所述，当使用 JavaScript 承诺或 TypeScript 承诺时，为了使一个函数能够**等待**另一个函数，该函数本身必须是一个**异步**函数。因此，我们将**患者简**标记为**异步**的原因是。****

******一俟******

****好吧，让我们假设另一个版本的简可以像往常一样继续她的社交生活，即使约翰没有按时分娩！因此，这意味着约翰一拿到钱，他们就可以去打保龄球。****

****这同样适用于 JavaScript 承诺。你程序的一部分可以**监听**寻找**当**数据可用时**然后**它可以消费它。****

****这里我们将使用 **eagerJane** 来监听**sideinmejohn**告诉她他有钱，然后他们可以去打保龄球！****

****请注意，由于 **eagerJane** 并没有**等待**sideinmejohn**，即使**sideinmejohn**正在等待他的副业收入，我们也没有将她( **eagerJaneB** )标记为**异步**。******

****最后****

**显然，您现在可以使用 JavaScript 承诺，并在处理 TypeScript 承诺时应用相同的内容。如您所见，在处理 JavaScript 承诺或 TypeScript 承诺时，Jane 和您一样有两种选择:**

1.  **等待结果。**
2.  **当结果可用时，倾听并消费它们。**

****结论****

**这是如何处理 JavaScript 承诺和 TypeScript 承诺的简单解释。**

**说完了，直到下一个！**

*****快乐编码！*****

**你对学习 JavaScript 感兴趣吗？在这里结账类似牛逼的文章: [*相关文章*](https://bingeoncode.com/article/javascript/How%20to%20use%20JavaScript%20promises%20or%20Typescript%20promises#related-articles)**

***更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的**[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的**[***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*****