---
规则名: no-space-before-semi
布局: doc

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

Examples of **incorrect** code for this rule:



```js
var foo = "bar" ;

var foo = function() {} ;

var foo = function() {
} ;

var foo = 1 + 2 ;
```

Examples of **correct** code for this rule:

::: correct

```js
;(function(){}());

var foo = "bar";
```
