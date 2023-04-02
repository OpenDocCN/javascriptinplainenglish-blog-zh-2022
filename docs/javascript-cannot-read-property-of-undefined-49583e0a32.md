# 修复:JavaScript 中的“无法读取未定义的属性”错误

> 原文：<https://javascript.plainenglish.io/javascript-cannot-read-property-of-undefined-49583e0a32?source=collection_archive---------1----------------------->

![](img/c129de2b809a9e819024cd122f72d04d.png)

当您试图访问变量`undefined`的属性时，会出现“无法读取未定义的属性”错误。例如:

```
const obj = undefined;// TypeError: Cannot read properties of undefined (reading 'prop')
console.log(obj.prop);
```

若要修复“无法读取未定义的属性”错误，请在访问属性之前对变量使用可选的链接运算符。如果变量为`undefined`或`null`，操作员将立即返回`undefined`并阻止属性访问。

```
const obj = undefined;console.log(obj?.prop); // undefined// Also works for nested property access
console.log(obj?.prop1?.prop2); // undefined// Usage in if...else statements
if (obj?.prop) {
  console.log(obj.prop);
} else {
  console.log("Can't find 'prop' property in 'obj'");
}
```

使用括号符号进行属性访问时，可选的链接运算符也起作用:

```
const obj = undefined;console.log(obj?.['prop']); // undefinedconsole.log(obj?.['prop1']?.['prop2']); // undefined
```

这意味着我们可以在阵列上使用它:

```
const arr = undefined;console.log(arr?.[0]); // undefined// Array containing an object
console.log(arr?.[2]?.prop); // undefined
```

## 注意

在可选链接可用之前，避免此错误的唯一方法是手动检查嵌套层次结构中属性的每个包含对象的真实性，即:

```
const a = undefined;// Optional chaining
if (a?.b?.c?.d?.e) {
  console.log(`e: ${e}`);
}// No optional chaining
if (a && a.b && a.b.c && a.b.c.d && a.b.c.d.e) {
  console.log(`e: ${e}`);
}
```

【codingbeautydev.com】更新于[](https://codingbeautydev.com/blog/javascript-cannot-read-property-of-undefined?utm_source=medium&utm_medium=social&utm_campaign=blog-promo)

*每周获取 web 开发技巧和教程*

*![](img/b8db4799ac3fa2b55b41c7ca714bdf64.png)*

*[**订阅**](https://codingbeautydev.com/newsletter)*