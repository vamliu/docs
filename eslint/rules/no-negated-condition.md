---
规则名: no-negated-condition
规则类型: suggestion
---


Negated conditions are more difficult to understand. Code can be made more readable by inverting the condition instead.

## 规则详解

This rule disallows negated conditions in either of the following:

* `if` statements which have an `else` branch
* ternary expressions

此规则的 **错误** 代码实例：



```js
/*eslint no-negated-condition: "error"*/

if (!a) {
    doSomething();
} else {
    doSomethingElse();
}

if (a != b) {
    doSomething();
} else {
    doSomethingElse();
}

if (a !== b) {
    doSomething();
} else {
    doSomethingElse();
}

!a ? c : b
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-negated-condition: "error"*/

if (!a) {
    doSomething();
}

if (!a) {
    doSomething();
} else if (b) {
    doSomething();
}

if (a != b) {
    doSomething();
}

a ? b : c
```
