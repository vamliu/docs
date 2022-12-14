---
规则名: symbol-description
规则类型: suggestion
深入了解:
- https://www.ecma-international.org/ecma-262/6.0/#sec-symbol-description
---


The `Symbol` function may have an optional description:

```js
var foo = Symbol("some description");

var someString = "some description";
var bar = Symbol(someString);
```

Using `description` promotes easier debugging: when a symbol is logged the description is used:

```js
var foo = Symbol("some description");

> console.log(foo);
// Symbol(some description)
```

It may facilitate identifying symbols when one is observed during debugging.

## 规则详解

This rules requires a description when creating symbols.

## Examples

此规则的 **错误** 代码实例：



```js
/*eslint symbol-description: "error"*/
/*eslint-env es6*/

var foo = Symbol();
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint symbol-description: "error"*/
/*eslint-env es6*/

var foo = Symbol("some description");

var someString = "some description";
var bar = Symbol(someString);
```

## 禁用建议

This rule should not be used in ES3/5 environments.
In addition, this rule can be safely turned off if you don't want to enforce presence of `description` when creating Symbols.
