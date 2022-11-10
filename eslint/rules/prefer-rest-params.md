---
规则名: prefer-rest-params
规则类型: suggestion
关联规则:
- prefer-spread
---


There are rest parameters in ES2015.
We can use that feature for variadic functions instead of the `arguments` variable.

`arguments` does not have methods of `Array.prototype`, so it's a bit of an inconvenience.

## 规则详解

This rule is aimed to flag usage of `arguments` variables.

## Examples

此规则的 **错误** 代码实例：



```js
/*eslint prefer-rest-params: "error"*/

function foo() {
    console.log(arguments);
}

function foo(action) {
    var args = Array.prototype.slice.call(arguments, 1);
    action.apply(null, args);
}

function foo(action) {
    var args = [].slice.call(arguments, 1);
    action.apply(null, args);
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint prefer-rest-params: "error"*/

function foo(...args) {
    console.log(args);
}

function foo(action, ...args) {
    action.apply(null, args); // or `action(...args)`, related to the `prefer-spread` rule.
}

// Note: the implicit arguments can be overwritten.
function foo(arguments) {
    console.log(arguments); // This is the first argument.
}
function foo() {
    var arguments = 0;
    console.log(arguments); // This is a local variable.
}
```

## 禁用建议

This rule should not be used in ES3/5 environments.

In ES2015 (ES6) or later, if you don't want to be notified about `arguments` variables, then it's safe to disable this rule.
