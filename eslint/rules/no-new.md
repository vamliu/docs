---
规则名: no-new
规则类型: suggestion
---


The goal of using `new` with a constructor is typically to create an object of a particular type and store that object in a variable, such as:

```js
var person = new Person();
```

It's less common to use `new` and not store the result, such as:

```js
new Person();
```

In this case, the created object is thrown away because its reference isn't stored anywhere, and in many cases, this means that the constructor should be replaced with a function that doesn't require `new` to be used.

## 规则详解

This rule is aimed at maintaining consistency and convention by disallowing constructor calls using the `new` keyword that do not assign the resulting object to a variable.

此规则的 **错误** 代码实例：



```js
/*eslint no-new: "error"*/

new Thing();
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-new: "error"*/

var thing = new Thing();

Thing();
```
