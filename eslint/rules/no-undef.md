---
规则名: no-undef
规则类型: problem
关联规则:
- no-global-assign
- no-redeclare
---



This rule can help you locate potential ReferenceErrors resulting from misspellings of variable and parameter names, or accidental implicit globals (for example, from forgetting the `var` keyword in a `for` loop initializer).

## 规则详解

Any reference to an undeclared variable causes a warning, unless the variable is explicitly mentioned in a `/*global ...*/` comment, or specified in the [`globals` key in the configuration file](../user-guide/configuring/language-options#using-configuration-files-1). A common use case for these is if you intentionally use globals that are defined elsewhere (e.g. in a script sourced from HTML).

此规则的 **错误** 代码实例：



```js
/*eslint no-undef: "error"*/

var foo = someFunction();
var bar = a + 1;
```

Examples of **correct** code for this rule with `global` declaration:

::: correct

```js
/*global someFunction, a*/
/*eslint no-undef: "error"*/

var foo = someFunction();
var bar = a + 1;
```

Note that this rule does not disallow assignments to read-only global variables.
See [no-global-assign](no-global-assign) if you also want to disallow those assignments.

This rule also does not disallow redeclarations of global variables.
See [no-redeclare](no-redeclare) if you also want to disallow those redeclarations.

## 配置项

* `typeof` set to true will warn for variables used inside typeof check (Default false).

### typeof

选项 default `{ "typeof": false }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-undef: "error"*/

if (typeof UndefinedIdentifier === "undefined") {
    // do something ...
}
```

You can use this option if you want to prevent `typeof` check on a variable which has not been declared.

选项 `{ "typeof": true }` 的 **错误** 代码示例：



```js
/*eslint no-undef: ["error", { "typeof": true }] */

if(typeof a === "string"){}
```

Examples of **correct** code for the `{ "typeof": true }` option with `global` declaration:

::: correct

```js
/*global a*/
/*eslint no-undef: ["error", { "typeof": true }] */

if(typeof a === "string"){}
```

## Environments

For convenience, ESLint provides shortcuts that pre-define global variables exposed by popular libraries and runtime environments. This rule supports these environments, as listed in [Specifying Environments](../user-guide/configuring/language-options#specifying-environments).  A few examples are given below.

### browser

Examples of **correct** code for this rule with `browser` environment:

::: correct

```js
/*eslint no-undef: "error"*/
/*eslint-env browser*/

setTimeout(function() {
    alert("Hello");
});
```

### Node.js

Examples of **correct** code for this rule with `node` environment:

::: correct

```js
/*eslint no-undef: "error"*/
/*eslint-env node*/

var fs = require("fs");
module.exports = function() {
    console.log(fs);
};
```

## 禁用建议

If explicit declaration of global variables is not to your taste.

## 兼容

This rule provides compatibility with treatment of global variables in [JSHint](http://jshint.com/) and [JSLint](http://www.jslint.com).
