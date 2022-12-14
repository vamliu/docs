---
规则名: valid-typeof
规则类型: problem
深入了解:
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof
---





For a vast majority of use cases, the result of the `typeof` operator is one of the following string literals: `"undefined"`, `"object"`, `"boolean"`, `"number"`, `"string"`, `"function"`, `"symbol"`, and `"bigint"`. It is usually a typing mistake to compare the result of a `typeof` operator to other string literals.

## 规则详解

This rule enforces comparing `typeof` expressions to valid string literals.

## 配置项

This rule has an object option:

* `"requireStringLiterals": true` requires `typeof` expressions to only be compared to string literals or other `typeof` expressions, and disallows comparisons to any other value.

此规则的 **错误** 代码实例：



```js
/*eslint valid-typeof: "error"*/

typeof foo === "strnig"
typeof foo == "undefimed"
typeof bar != "nunber"
typeof bar !== "fucntion"
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint valid-typeof: "error"*/

typeof foo === "string"
typeof bar == "undefined"
typeof foo === baz
typeof bar === typeof qux
```

Examples of **incorrect** code with the `{ "requireStringLiterals": true }` option:



```js
/*eslint valid-typeof: ["error", { "requireStringLiterals": true }]*/

typeof foo === undefined
typeof bar == Object
typeof baz === "strnig"
typeof qux === "some invalid type"
typeof baz === anotherVariable
typeof foo == 5
```

Examples of **correct** code with the `{ "requireStringLiterals": true }` option:

::: correct

```js
/*eslint valid-typeof: ["error", { "requireStringLiterals": true }]*/

typeof foo === "undefined"
typeof bar == "object"
typeof baz === "string"
typeof bar === typeof qux
```

## 禁用建议

You may want to turn this rule off if you will be using the `typeof` operator on host objects.
