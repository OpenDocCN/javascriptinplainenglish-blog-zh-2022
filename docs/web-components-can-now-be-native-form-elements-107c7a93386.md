# Web 组件现在可以是本机表单元素

> 原文：<https://javascript.plainenglish.io/web-components-can-now-be-native-form-elements-107c7a93386?source=collection_archive---------1----------------------->

## 这是定制表单控件的完整指南

![](img/a2a64266a9dd589fdd0345685a0fde58.png)

Photo by [Chris Hainto](https://unsplash.com/@chrishainto?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 自定义表单控件

开发人员一直想定制元素的一个领域是表单。

从历史上看，通常很难对窗体控件进行样式化，以使它们具有您想要的外观和感觉。

样式选项通常是有限的，直到今天，像日期和颜色选择器这样的表单控件在不同的浏览器中仍然不一致。

许多网站还需要更高级的表单控件，而本地平台还没有提供。

Web 组件是定制表单控件的理想选择，因为它们是一流的 HTML 标签，但不幸的是，它们不提供开箱即用的内置表单控件的功能。

例如，提交表单时，用自定义元素构建的自定义表单控件不包含在表单数据中。

表单验证和自动填充等其他功能也无法用于自定义元素，并且很难复制。

幸运的是，这些问题有两种解决方案:事件`formdata`和接口`ElementInternals`。

# FormData 事件

提交表单时会触发`formdata`事件，该事件允许任何 JavaScript 代码向提交的表单数据中添加任意数据。

您可以为这个事件设置一个事件监听器，它将接收带有`formData`属性的事件对象，该属性包含表单提交的所有数据。

然后，每个事件侦听器可以在提交数据之前添加或修改数据:

```
const form = document.querySelector(‘form’);
form.addEventListener(‘formdata’, ({formData}) => {// add data
 formData.append(‘custom-control’, customValue);// modify data
 formData.set(‘email’, formData.get(‘email’).toLowerCase());
});
```

事件的`formData`属性是一个 [FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData) 对象。

# 元素内部接口

虽然`formData`事件非常方便，但它仅限于向表单提交的数据中添加任意数据。

要使自定义元素成为真正的表单控件，它还应该自动与表单关联并参与表单验证。

这就是`ElementInternals`接口的用途。

它允许自定义元素与表单相关联，因此它们被添加到表单的`elements`属性中，元素的值将自动与表单一起提交。

它还使自定义元素能够参与表单验证。

该元素可以指示其值是有效还是无效，并防止表单在无效时被提交。

它也可以用一个`<label>`元素来标记，这意味着标签以编程方式与表单元素相关联。

当用户单击或点击标签时，表单元素将获得焦点。

这增加了关注提供良好用户体验的元素的区域，尤其是在移动设备上。

当用户关注表单元素时，它还会使屏幕阅读器读出标签。

# 将自定义元素与表单相关联

创建带有自定义元素的自定义窗体控件的第一步是将其与窗体相关联。

这意味着它将是表单的`elements`属性的一部分，该属性是一个包含表单包含的所有表单控件的`HTMLFormControlsCollection`。

在前面的例子中，您已经看到了如何使用`append`方法向`FormData`对象添加条目。

也可以通过将表单传递给`FormData`构造函数，直接从表单中的所有元素及其值创建一个`FormData`对象:

```
const form = document.querySelector(‘form’); // formData now contains all data of form
const formData = new FormData(form);
```

`formData`现在包含表单的所有数据，包括已经与表单关联的任何自定义元素。

下面是一个与表单相关的定制元素的`class`:

```
class FormInput extends HTMLElement {
  static formAssociated = true;

  constructor() {
    super();
    this.internals = this.attachInternals();
  } get value() {
    return this._value;
  } set value(value) {
    this._value = value;
    this.internals.setFormValue(value);
  } get form() {
    return this.internals.form;
  }

  get name() {
    return this.getAttribute(‘name’);
  }

  get type() {
    return this.localName;
  }
}
```

此示例显示了一个与窗体关联的自定义元素的最小实现。让我们来看看各个部分。

```
static formAssociated = true;
```

通过将静态`formAssociated`属性设置为`true`，自定义元素将与表单相关联，并且将包含在表单的`elements`属性中。

然而，这还不包括表单数据中自定义元素的值。

为此，需要将`ElementInternals`接口附加到元素上:

```
this.internals = this.attachInternals();
```

`attachInternals`返回`ElementInternals`对象，然后存储在自定义元素的`internals`属性中。

为了获得将与表单一起提交的自定义元素的值，需要使用以下内容来设置该值:

```
this.internals.setFormValue(value);.
```

在示例中，这一行被添加到了`value`属性的设置器中，以确保无论何时设置了`value`，其表单值也将被设置。

这是将与表单一起提交的值。

用于`form`、`name`和`type`的其他 getters 是本地表单元素所具有的标准属性。

*这是你的组件成为定制表单元素的最低要求。*

当然，这个组件还没有呈现任何东西，所以它不是很有用。让我们通过添加一个带有`<input>`元素的阴影根来改变它:

```
constructor() {
  super();
  this.internals = this.attachInternals(); const shadowRoot = this.attachShadow({mode: ‘open’}); shadowRoot.innerHTML = `
    <style>
      :host {
        display: inline-block;
      } input {
        display: block;
        padding: 5px;
      }
    </style> <input type=”text”>
 `;
}
```

既然组件有了一个`<input>`，我们首先需要确保输入的值可以作为表单中提交的组件的值。

回想一下，我们为调用`this.internals.setFormValue(value)`的`value`属性创建了一个 setter。

我们可以通过它的`change`事件得到每次输入改变时的值。

当该事件被触发时，我们只需设置组件的`value`属性，该属性将调用调用`this.internals.setFormValue(value)`的 setter。

让我们添加所需的事件监听器:

```
this.input = this.shadowRoot.querySelector(‘input’);this.input.addEventListener(‘change’, (e) => {
  this.value = this.input.value;
});
```

现在，每次输入的值发生变化时，组件的值都会更新，正确的值会随表单一起提交。

当然，反过来也应该可以:当组件的`value`属性被设置时，`<input>`的`value`属性也应该被设置。

设置器应改为:

```
set value(value) {
  this._value = value;
  this.input.value = value; // set the value of the input 
  this.internals.setFormValue(value);
}
```

使用我们组件的代码也将期望触发一个`change`事件，因为它现在包含了一个`<input>`元素。

因此，来自`<input>`的`event`应该被转发。

我们不能简单地再次调度它，因为这将抛出一个错误，表明事件已经被调度，但我们可以克隆它，然后转发它:

```
this.input.addEventListener(‘change’, (e) => {
  const clone = new e.constructor(e.type, e); // clone the event this.dispatchEvent(clone); // and then forward it this.value = this.input.value;
});
```

现在组件的值和输入保持同步，组件触发了一个`change`事件。

# 标记自定义窗体控件

既然您已经将您的定制元素与表单相关联，那么您也可以将它与一个`<label>`相关联。

这样做的好处是，自定义元素也将通过编程方式与标签相关联。

这意味着，例如，当用户聚焦输入时，屏幕阅读器将读出标签文本，并且当标签被点击或轻击时，相关联的输入将被聚焦。

这增加了输入的触摸面积，使其更容易聚焦，尤其是在移动设备上。

有两种方法可以将表单控件与`<label>`相关联。

最简单的方法是将表单控件放在`<label>`中。

这使得这种关联非常明显:

```
<label>
  City
  <input type=”text” name=”city”>
</label>
```

另一种方法是使用`<label>`的`for`属性。

该属性的值应该是您要与之关联的表单控件的`id`:

```
<label for=”city”>City</label>
<input type=”text” id=”city”>
```

当标签和表单控件在 DOM 中的不同位置，或者由于某种原因不能将控件放在标签中时，这可能会很方便。

在定制表单控件中点击标签焦点`<input>`还需要做两件事情。

首先，组件应该是可聚焦的。这是通过添加一个`tabindex`属性来完成的。

此属性指示元素是可聚焦的，以及当用户使用 TAB 键在表单控件中导航时元素聚焦的顺序。

通常，焦点顺序依赖于元素在 DOM 中出现的顺序，但是使用`tabindex`可以改变这种顺序。

这意味着，例如，具有`tabindex` 4 的元素将被聚焦在具有`tabindex` 5 的元素之前，但是在具有`tabindex` 3 的元素之后。

当两个元素有相同的`tabindex`时，DOM 中的顺序优先，所以如果你想保持这个顺序，但需要添加`tabindex`使元素可聚焦，你可以对所有元素使用`tabindex="0"`。

为了确保元素总是有一个`tabindex`属性，您可以检查它是否存在，如果不存在就添加它:

```
if (!this.hasAttribute(‘tabindex’)) {
  this.setAttribute(‘tabindex’, ‘0’);
}
```

现在你的组件是可聚焦的了，当它关联的`<label>`被点击或轻击时，它将被聚焦。

但是因为它里面的`<input>`需要被聚焦，所以焦点应该用下面的代码来委托:

```
this.addEventListener(‘focus’, () => this.input.focus());
```

现在，当点击`<label>`时，组件内的`<input>`将被聚焦。

这是完整的组件:

```
class FormInput extends HTMLElement {
  static formAssociated = true; constructor() {
    super();
    this.internals = this.attachInternals(); const shadowRoot = this.attachShadow({mode: ‘open’}); shadowRoot.innerHTML = `
      <style>
        :host {
          display: inline-block;
        } input {
          display: block;
          padding: 5px;
        }
      </style> <input type=”text”>
   `;
 } connectedCallback() {
    this.input = this.shadowRoot.querySelector(‘input’); this.input.addEventListener(‘change’, (e) => {
      const clone = new e.constructor(e.type, e); this.dispatchEvent(clone); this.value = this.input.value;
    }); this.addEventListener(‘focus’, () => this.input.focus()); if (!this.hasAttribute(‘tabindex’)) {
      this.setAttribute(‘tabindex’, ‘0’);
    }
  } get value() {
    return this._value;
  } set value(value) {
    this._value = value;
    this.internals.setFormValue(value);
  } get form() {
    return this.internals.form;
  }

  get name() {
    return this.getAttribute(‘name’);
  }

  get type() {
    return this.localName;
  }
}
```

这是一个可用的密码笔:

Custom Element form control

请务必阅读我的后续文章[解释 Web 组件如何参与原生表单验证。](https://medium.com/itnext/native-form-validation-of-web-components-a599e85176c7)

在 Twitter 上关注我，在那里我写了现代网络能做什么，PWAs，和网络组件。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。*