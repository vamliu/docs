---
规则名: no-unneeded-ternary
规则类型: suggestion
关联规则:
- no-ternary
- no-nested-ternary
---



It's a common mistake in JavaScript to use a conditional expression to select between two Boolean values instead of using ! to convert the test to a Boolean.
Here are some examples:

```js
// 错误
var isYes = answer === 1 ? true : false;

// 正确
var isYes = answer === 1;

// 错误
var isNo = answer === 1 ? false : true;

// 正确
var isNo = answer !== 1;
```

Another common mistake is using a single variable as both the conditional test and the consequent. In such cases, the logical `OR` can be used to provide the same functionality.
Here is an example:

```js
// 错误
foo(bar ? bar : 1);

// 正确
foo(bar || 1);
```

## 规则详解

This rule disallow ternary operators when simpler alternatives exist.

此规则的 **错误** 代码实例：



```js
/*eslint no-unneeded-ternary: "error"*/

var a = x === 2 ? true : false;

var a = x ? true : false;
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-unneeded-ternary: "error"*/

var a = x === 2 ? "Yes" : "No";

var a = x !== false;

var a = x ? "Yes" : "No";

var a = x ? y : x;

f(x ? x : 1); // default assignment - would be disallowed if defaultAssignment option set to false. See option details below.
```

## 配置项

This rule has an object option:

* `"defaultAssignment": true` (default) allows the conditional expression as a default assignment pattern
* `"defaultAssignment": false` disallows the conditional expression as a default assignment pattern

### defaultAssignment

When set to `true`, which it is by default, The defaultAssignment option allows expressions of the form `x ? x : expr` (where `x` is any identifier and `expr` is any expression).

Examples of additional **incorrect** code for this rule with the `{ "defaultAssignment": false }` option:



```js
/*eslint no-unneeded-ternary: ["error", { "defaultAssignment": false }]*/

var a = x ? x : 1;

f(x ? x : 1);
```

Note that `defaultAssignment: false` still allows expressions of the form `x ? expr : x` (where the identifier is on the right hand side of the ternary).

## 禁用建议

You can turn this rule off if you are not concerned with unnecessary complexity in conditional expressions.
