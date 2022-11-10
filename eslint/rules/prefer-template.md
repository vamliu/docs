---
规则名: prefer-template
规则类型: suggestion
关联规则:
- no-useless-concat
- quotes
---



In ES2015 (ES6), we can use template literals instead of string concatenation.

```js
var str = "Hello, " + name + "!";
```

```js
/*eslint-env es6*/

var str = `Hello, ${name}!`;
```

## 规则详解

This rule is aimed to flag usage of `+` operators with strings.

## Examples

此规则的 **错误** 代码实例：



```js
/*eslint prefer-template: "error"*/

var str = "Hello, " + name + "!";
var str = "Time: " + (12 * 60 * 60 * 1000);
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint prefer-template: "error"*/
/*eslint-env es6*/

var str = "Hello World!";
var str = `Hello, ${name}!`;
var str = `Time: ${12 * 60 * 60 * 1000}`;

// This is reported by `no-useless-concat`.
var str = "Hello, " + "World!";
```

## 禁用建议

This rule should not be used in ES3/5 environments.

In ES2015 (ES6) or later, if you don't want to be notified about string concatenation, you can safely disable this rule.
