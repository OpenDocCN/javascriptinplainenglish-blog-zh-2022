# JavaScript Promise 和 JavaScript Observable——有什么区别？

> 原文：<https://javascript.plainenglish.io/javascript-promise-vs-javascript-observable-what-is-the-difference-8d98987e8781?source=collection_archive---------1----------------------->

## 了解什么是 JavaScript promise 和 JavaScript observable，知道它们的区别。

![](img/2e1e41ae9ba2005c76b3e54357bab642.png)

JavaScript promise vs JavaScript observable — what is the difference?

您的应用程序所需的数据不会立即可用。这就是 JavaScript promise vs JavaScript observable 的由来。

任何现代的应用程序总是需要有一种方式使 ***反应*** 。这意味着您的应用程序应该意识到来自用户操作的数据更改和更新，并以预期的方式做出反应。出于这个原因，有两种主要的方法来解决这个问题，因此，您可能认为需要在 JavaScript promise 和 JavaScript observable 之间做出决定。

这篇简短的教程提示将为你解决这个争论。在本教程结束时，您将会警惕下一次遇到 JavaScript promise vs JavaScript observable 困境时如何继续。

首先，回答你的问题，JavaScript promise 和 JavaScript observable 哪个更好用，答案也很简单。**这完全取决于你的预期用例**。我可能打破了你的幻想，但有时，现实往往令人失望(*灭霸——疯狂的泰坦*)。所以，你现在应该考虑哪个**最适合你的用例**，而不是 JavaScript promise 和 JavaScript observable。

我知道你在这里是为了清晰地讨论 JavaScript 承诺和 JavaScript 可观察性，但是请耐心等待。

现在，继续的最好方法是理解什么是 JavaScript 承诺，什么是 JavaScript 可观察。所以我们现在把思维模式从 JavaScript promise vs JavaScript observable 转移到它们各自是什么，这样就有可能在你应该使用哪个的时候做出正确的决定。

但是我们将用非常简单明了的英语来做这件事——是的，用简单明了的英语来写 JavaScript！让我们来回答这两个问题:

## 1.什么是承诺

承诺就是把你自己放在那里，承诺一旦你有能力，你就会去做一些事情。

你也可以对自己承诺，一旦你开始健身，你就会停止吃垃圾食品。

## 2.什么/谁是观察者

把观察者想象成观察变化的人，然后他们向必要的权威汇报。

你可以观察自己的体重，并在每次进出健身房时记下笔记，这样你就可以**关注**自己的体重变化，从而计算出你的基础代谢率等。

因此，在理解了什么是承诺和什么是观察者之后，现在让我们将上述理解直接映射到 JavaScript 反应式编程环境中。那么，让我们来看看:

## 1.什么是 JavaScript 承诺

JavaScript promise 是一个承诺声明，一旦数据可用，您将把它提供给**承诺方**并结清该承诺的债务。**一旦债务结清，事情就结束了。这仅做一次。**

## 2.什么是 JavaScript 可观察值

一个 JavaScript observable 就是每次数据可用时，你总是向**观察方提供数据。然而，您向**订阅方**提供数据的能力将达到该方不再需要您的数据的程度。**

因此，在理解了什么是 JavaScript promise 和什么是 JavaScript observable 之后，最好看看在哪里使用它们的示例用例，也许每个用例都有一个代码样本。

现在让我们看一些 JavaScript promise vs JavaScript observable 教程的例子。

## JavaScript 承诺的用例示例。

假设您想要登录到您的用户，**然后**一旦用户登录，您将会用一个漂亮的通知消息来欢迎他们。我们可以用一个简单的承诺。

```
/**
 * 
 * @param email 
 * @param password 
 * 
 * login user using their email and password 
 */
function loginUser(
    email: string,
    password: string
) {
    const resource = new Request(`https://your-backend-endpoint/login`)
    const formData = new FormData();
    formData.set('email', email);
    formData.set('password', password);
    return fetch(resource, {method: 'POST', mode: 'cors', body: formData}).then(
        response => {
            if (!response.ok) {
                return Promise.reject('Invalid credentials!');
            }
            return response.json();
        }
    ).then(response => {
        return Promise.resolve(response);
    })
}

/**
 * 
 * @param email 
 * @param password 
 * 
 * hypothetically, when the user clicks the login button, pass in the value for
 * email and password.
 */
function doLogin(email: string, password: string) {
    loginUser(email, password).then(res => {
        alert(`Hi there ${res.fullName}`)
    }).catch(err => {
        alert('Oooops! Invalid credentials provided')
    });
}
```

现在让我们看看 JavaScript 承诺与 JavaScript 可观察性讨论的下一个选项。

## JavaScript 可观察的用例示例

因此，一旦您上面的用户登录，那么让我们假设他们有一个部分，他们需要将当天的销售线索添加为电话号码，然后将这些显示在 UI 上。UI 将**订阅**输入的数字，然后更新以反映这些变化。

```
/**
 * This is a mock hypothetical component, and for this case, we are using Angular.
 * 
 * This will give you a better understanding on how powerful JavaScript observables are.
 */
@Component({
    selector: 'app-leads-component'
})
export class LeadsComponent {

    /**
     * A list of leads
     */
    private _myLeads: Array;

    /**
     * A BehaviourSubject is an observable which is imported from RXJS.
     * 
     * It makes it possible to populate your initial data, with something
     * which you can present to the UI, and have it updated with time.
     */
    public myLeads$: BehaviourSubject> = new BehaviourSubject>([]);

    constructor(
        private _yourBackendService: YourBackendService
    ) {}

    /**
     * when the component intialized
     */
    ngOnInit() {
        this._listenForLeadsFromBackend();
    }

    /**
     * listen for the list of leads user currently has in their backend,
     * and this will fetch the leads only once when the component is
     * initialized.
     * 
     * IF you want to have the event for new leads from the backend, then in
     * that case, you will have to go the WebSocket way, which is out of the scope of this tutorial
     */
    private _listenForLeadsFromBackend(): void {
        this._yourBackendService.getLeads().subscribe(
            /**
             * 
             * @param leads 
             * 
             * here, update the list of your leads with the received leads from the server
             * then set the next value for myLeads$ to your _myLeads
             */
            (leads: Array) => {
                this._myLeads = leads;
                this.updateMyLeadsObservable();
            }
        )
    }

    /**
     * 
     * @param number 
     * @param name 
     * 
     * add a lead number by inputting it and then updating on the UI all
     * the leads
     */
    public addCustomerLeadNumber(number: string, name: string) {
        this._myLeads.push(new Lead(number, name));
        this.updateMyLeadsObservable();
    }

    /**
     * common method for updating my leads observable
     */
    public updateMyLeadsObservable(): void {
        this.myLeads$.next(this._myLeads);
    }
}
```

显然，您可以看到 JavaScript observable 对于那些需要的反应式编程特性来说非常方便，尽管需要更多的代码。

所以，不要再想 JavaScript promise vs JavaScript observable 了，想想你的用例吧。

## 结论

所以，你现在可以看到，这不是 JavaScript 承诺和 JavaScript 可观察性的问题，而是哪个最适合你的用例的问题。

所以，下一次你想对你的代码进行反应式编程时，你现在可以轻松地在 JavaScript promise 或 JavaScript observable 之间进行选择。

这篇简短的 JavaScript promise vs JavaScript observable 教程只是 JavaScript promise 和 JavaScript observable 惊人能力的表面现象。请随意探索，了解更多关于这些令人敬畏和干净的反应式编程方法。

让我知道你对 JavaScript promise vs JavaScript observable 这篇文章的看法。

请随意与您的朋友分享这一点，并帮助他们解决 JavaScript 承诺与 JavaScript 可观察性之间的困境。

嗯，直到下一篇！

***快乐编码！***

*有兴趣学习****JavaScript****吗？在这里结帐类似的牛逼文章:* [*相关文章*](https://bingeoncode.com/article/javascript/javascript%20promise%20vs%20javascript%20observable%20%E2%80%93%20what%20is%20the%20difference%3F#related-articles)

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *。***