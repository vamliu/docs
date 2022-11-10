---
规则名: no-space-before-semi

关联规则:
- semi
- no-extra-semi
---

Disallows spaces before semicolons.

(removed) This rule was **removed** in ESLint v1.0 and **replaced** by the [semi-spacing](semi-spacing) rule.

JavaScript allows for placing unnecessary spaces between an expression and the closing semicolon.

Space issues can also cause code to look inconsistent and harder to read.

```js
var thing = function () {
  var test = 12 ;
}  ;
```

## 规则详解

This rule prevents the use of spaces before a semicolon in expressions.

此规则的 **错误** 代码实例：



```js
var foo = "bar" ;

var foo = function() {} ;

var foo = function() {
} ;

var foo = 1 + 2 ;
```

此规则的 **正确** 代码实例：

::: correct

```js
;(function(){}());

var foo = "bar";
```
