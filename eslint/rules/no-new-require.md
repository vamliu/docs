---
规则名: no-new-require
规则类型: suggestion
---


This rule was **deprecated** in ESLint v7.0.0. Please use the corresponding rule in [`eslint-plugin-node`](https://github.com/mysticatea/eslint-plugin-node).

The `require` function is used to include modules that exist in separate files, such as:

```js
var appHeader = require('app-header');
```

Some modules return a constructor which can potentially lead to code such as:

```js
var appHeader = new require('app-header');
```

Unfortunately, this introduces a high potential for confusion since the code author likely meant to write:

```js
var appHeader = new (require('app-header'));
```

For this reason, it is usually best to disallow this particular expression.

## 规则详解

This rule aims to eliminate use of the `new require` expression.

此规则的 **错误** 代码实例：



```js
/*eslint no-new-require: "error"*/

var appHeader = new require('app-header');
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-new-require: "error"*/

var AppHeader = require('app-header');
var appHeader = new AppHeader();
```

## 禁用建议

If you are using a custom implementation of `require` and your code will never be used in projects where a standard `require` (CommonJS, Node.js, AMD) is expected, you can safely turn this rule off.
