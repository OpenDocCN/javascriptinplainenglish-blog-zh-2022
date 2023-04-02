# 你应该知道的打字稿要点

> 原文：<https://javascript.plainenglish.io/typescript-essentials-you-should-know-d026f9e88bc1?source=collection_archive---------7----------------------->

## 学习这些基础知识可以更好地利用 TypeScript。

![](img/860d67ccdfd561337c7cd60704f9e72d.png)

Photo by [Todd Quackenbush](https://unsplash.com/@toddquackenbush?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

这篇文章涵盖了 TypeScript 的一些基础知识，人们可以考虑学习这些知识来更好地使用这种语言。

## 接口和类型

在 TypeScript 中，接口和类型是在代码中定义协定以及与项目外部的代码定义协定的强大方法。

除了在用法和实现上有一些小的不同，它们大部分都是相似的。

1.  **延伸**

界面:

```
 interface Animal{
  name:string;
}interface Bear **extends Animal**{
  honey: boolean;
}const bear: Bear = getBear(); // getBear returns Bear
bear.name;
bear.honey;
```

类型:

```
type Animal = {
  name:string;
}type Bear = Animal **&** {
  honey: boolean;
}const bear: Bear = getBear(); // getBear returns Bear
bear.name;
bear.honey;
```

2.**修改字段**

接口:可以向现有接口添加新字段。

```
interface Window{
  title:string;
}interface Window{
  name:string
}// Now interface Window has both title and name
```

类型:创建后不能更改。

```
type Window{
  title:string;
}type Window{
  name:string
}// Error Duplicate Identifier Window
```

## keyof 类型运算符

该操作符接受一个对象，并生成其键的字符串或数字文字并集。

```
type Person = { name: string, age: number }
type PersonType = keyof Person; // name | age
```

## typeof 类型运算符

typeof 可在类型上下文中用于引用变量或属性的类型。

```
Example 1: 
let name = 'John';
let NType: typeof name; // NType is string Example 2:
let person = {
  code:"1", name:"Rahul"
}let employee: **typeof** person;employee = { code:"2", name:"Sachin"};    *//OK*employee = { code: "2", name: "Sachin", salary: 1000 }; *//* ***ErrorType '{ code: string; name: string; salary: number; }' is not assignable to type '{ code: string; name: string; }'***
```

## 索引访问类型

我们可以使用这种类型来查找另一种类型的特定属性。

```
type Person = { name: string, age: number, isMale: boolean };type PType = Person[keyof Person]; 
// string | number | boolean
```

## 映射类型

可用于创建基于另一个类型的类型。

```
type OptionalFlags<T> = {
    [Property in keyof T]:boolean;
}type FeatureFlags = {
    darkMode: () => void;
    profile: () => void;
}type FeatureOptions = OptionalFlags<FeatureFlags>;
// { darkMode: boolean, profile: boolean }
```

## 映射修改器

有两个额外的修饰符可以在映射期间应用:`readonly`和`?`，它们分别影响可变性和可选性。

您可以通过在它们前面加上`-`或`+`来删除或添加这些修饰符。如果不加前缀，那么就假定为`+`。

```
// Removes 'readonly' attributes from a type's propertiestype CreateMutable<T> = {
    -readonly[Property in keyof T]:T[Property]
}type LockedAccount = {
    readonly id: string;
    readonly name: string;
}type UnlockedAccount = CreateMutable<LockedAccount>;
// { id: string; name: string } 
**// notice readonly has been removed**
```

## 通过“as”重新映射键

在 TypeScript 4.1 及更高版本中，您可以使用映射类型中的`as`子句来重新映射映射类型中的键:

```
**type MappedWithNewProperties<T> = {
    [Properties in keyof T as NewKeyType]: T[Properties]
}**
```

例如

```
type Getters<T> = {
  [Property in keyof T as `get${Capitalize<string & Property>}`]: () => T[Property]
};interface Person {
    name: string;
    age: number;
}type LazyPerson = Getters<Person>;
// { getName: () => string; getAge: () => number }
```

这个题目到此为止。感谢您的阅读。

 [## 学习 TypeScript 的起点

### 查找 TypeScript 入门项目:从 Angular 到 React 或者 Node.js 和 CLIs。

www.typescriptlang.org](https://www.typescriptlang.org/docs/) 

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。***