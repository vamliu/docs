---
规则名: no-new-symbol
规则类型: problem
深入了解:
- https://www.ecma-international.org/ecma-262/6.0/#sec-symbol-objects
---



`Symbol` is not intended to be used with the `new` operator, but to be called as a function.

```js
var foo = new Symbol("foo");
```

This throws a `TypeError` exception.

## 规则详解

This rule is aimed at preventing the accidental calling of `Symbol` with the `new` operator.

## Examples

此规则的 **错误** 代码实例：



```js
/*eslint no-new-symbol: "error"*/
/*eslint-env es6*/

var foo = new Symbol('foo');
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-new-symbol: "error"*/
/*eslint-env es6*/

var foo = Symbol('foo');

// Ignores shadowed Symbol.
function bar(Symbol) {
    const baz = new Symbol("baz");
}

```

## 禁用建议

This rule should not be used in ES3/5 environments.
