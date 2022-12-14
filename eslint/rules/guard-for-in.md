---
规则名: guard-for-in
规则类型: suggestion
关联规则:
- no-prototype-builtins
深入了解:
- https://javascriptweblog.wordpress.com/2011/01/04/exploring-javascript-for-in-loops/
- https://2ality.com/2012/01/objects-as-maps.html
---


Looping over objects with a `for in` loop will include properties that are inherited through the prototype chain. This behavior can lead to unexpected items in your for loop.

```js
for (key in foo) {
    doSomething(key);
}
```

Note that simply checking `foo.hasOwnProperty(key)` is likely to cause an error in some cases; see [no-prototype-builtins](no-prototype-builtins).

## 规则详解

This rule is aimed at preventing unexpected behavior that could arise from using a `for in` loop without filtering the results in the loop. As such, it will warn when `for in` loops do not filter their results with an `if` statement.

此规则的 **错误** 代码实例：



```js
/*eslint guard-for-in: "error"*/

for (key in foo) {
    doSomething(key);
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint guard-for-in: "error"*/

for (key in foo) {
    if (Object.prototype.hasOwnProperty.call(foo, key)) {
        doSomething(key);
    }
}

for (key in foo) {
    if ({}.hasOwnProperty.call(foo, key)) {
        doSomething(key);
    }
}
```
