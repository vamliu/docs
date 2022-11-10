---
规则名: no-func-assign
规则类型: problem
---



JavaScript functions can be written as a FunctionDeclaration `function foo() { ... }` or as a FunctionExpression `var foo = function() { ... };`. While a JavaScript interpreter might tolerate it, overwriting/reassigning a function written as a FunctionDeclaration is often indicative of a mistake or issue.

```js
function foo() {}
foo = bar;
```

## 规则详解

This rule disallows reassigning `function` declarations.

此规则的 **错误** 代码实例：



```js
/*eslint no-func-assign: "error"*/

function foo() {}
foo = bar;

function foo() {
    foo = bar;
}

var a = function hello() {
  hello = 123;
};
```

Examples of **incorrect** code for this rule, unlike the corresponding rule in JSHint:



```js
/*eslint no-func-assign: "error"*/

foo = bar;
function foo() {}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-func-assign: "error"*/

var foo = function () {}
foo = bar;

function foo(foo) { // `foo` is shadowed.
    foo = bar;
}

function foo() {
    var foo = bar;  // `foo` is shadowed.
}
```
