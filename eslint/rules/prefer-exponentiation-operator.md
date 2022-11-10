---
规则名: prefer-exponentiation-operator
规则类型: suggestion
深入了解:
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Exponentiation
- https://bugs.chromium.org/p/v8/issues/detail?id=5848
---



Introduced in ES2016, the infix exponentiation operator `**` is an alternative for the standard `Math.pow` function.

Infix notation is considered to be more readable and thus more preferable than the function notation.

## 规则详解

This rule disallows calls to `Math.pow` and suggests using the `**` operator instead.

此规则的 **错误** 代码实例：



```js
/*eslint prefer-exponentiation-operator: "error"*/

const foo = Math.pow(2, 8);

const bar = Math.pow(a, b);

let baz = Math.pow(a + b, c + d);

let quux = Math.pow(-1, n);
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint prefer-exponentiation-operator: "error"*/

const foo = 2 ** 8;

const bar = a ** b;

let baz = (a + b) ** (c + d);

let quux = (-1) ** n;
```

## 禁用建议

This rule should not be used unless ES2016 is supported in your codebase.
