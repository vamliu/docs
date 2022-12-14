---
规则名: max-statements-per-line
规则类型: layout
关联规则:
- max-depth
- max-len
- max-lines
- max-lines-per-function
- max-nested-callbacks
- max-params
- max-statements
---


A line of code containing too many statements can be difficult to read. Code is generally read from the top down, especially when scanning, so limiting the number of statements allowed on a single line can be very beneficial for readability and maintainability.

```js
function foo () { var bar; if (condition) { bar = 1; } else { bar = 2; } return true; } // too many statements
```

## 规则详解

This rule enforces a maximum number of statements allowed per line.

## 配置项

### max

The "max" object property is optional (default: 1).

选项 `{ "max": 1 }`  默认值的 **错误** 代码示例：



```js
/*eslint max-statements-per-line: ["error", { "max": 1 }]*/

var bar; var baz;
if (condition) { bar = 1; }
for (var i = 0; i < length; ++i) { bar = 1; }
switch (discriminant) { default: break; }
function foo() { bar = 1; }
var foo = function foo() { bar = 1; };
(function foo() { bar = 1; })();
```

选项 `{ "max": 1 }` 默认值的 **正确** 代码示例：

::: correct

```js
/*eslint max-statements-per-line: ["error", { "max": 1 }]*/

var bar, baz;
if (condition) bar = 1;
for (var i = 0; i < length; ++i);
switch (discriminant) { default: }
function foo() { }
var foo = function foo() { };
(function foo() { })();
```

选项 `{ "max": 2 }` 的 **错误** 代码示例：



```js
/*eslint max-statements-per-line: ["error", { "max": 2 }]*/

var bar; var baz; var qux;
if (condition) { bar = 1; } else { baz = 2; }
for (var i = 0; i < length; ++i) { bar = 1; baz = 2; }
switch (discriminant) { case 'test': break; default: break; }
function foo() { bar = 1; baz = 2; }
var foo = function foo() { bar = 1; };
(function foo() { bar = 1; baz = 2; })();
```

选项 `{ "max": 2 }` 的 **正确** 代码示例：

::: correct

```js
/*eslint max-statements-per-line: ["error", { "max": 2 }]*/

var bar; var baz;
if (condition) bar = 1; if (condition) baz = 2;
for (var i = 0; i < length; ++i) { bar = 1; }
switch (discriminant) { default: break; }
function foo() { bar = 1; }
var foo = function foo() { bar = 1; };
(function foo() { var bar = 1; })();
```

## 禁用建议

You can turn this rule off if you are not concerned with the number of statements on each line.
