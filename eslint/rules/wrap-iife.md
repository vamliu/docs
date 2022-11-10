---
规则名: wrap-iife
规则类型: layout
---



You can immediately invoke function expressions, but not function declarations. A common technique to create an immediately-invoked function expression (IIFE) is to wrap a function declaration in parentheses. The opening parentheses causes the contained function to be parsed as an expression, rather than a declaration.

```js
// function expression could be unwrapped
var x = function () { return { y: 1 };}();

// function declaration must be wrapped
function () { /* side effects */ }(); // SyntaxError
```

## 规则详解

This rule requires all immediately-invoked function expressions to be wrapped in parentheses.

## 配置项

This rule has two options, a string option and an object option.

String option:

* `"outside"` enforces always wrapping the *call* expression. The default is `"outside"`.
* `"inside"` enforces always wrapping the *function* expression.
* `"any"` enforces always wrapping, but allows either style.

Object option:

* `"functionPrototypeMethods": true` additionally enforces wrapping function expressions invoked using `.call` and `.apply`. The default is `false`.

### outside

选项 default `"outside"` 的 **错误** 代码示例：



```js
/*eslint wrap-iife: ["error", "outside"]*/

var x = function () { return { y: 1 };}(); // unwrapped
var x = (function () { return { y: 1 };})(); // wrapped function expression
```

选项 default `"outside"` 的 **正确** 代码示例：

::: correct

```js
/*eslint wrap-iife: ["error", "outside"]*/

var x = (function () { return { y: 1 };}()); // wrapped call expression
```

### inside

选项 `"inside"` 的 **错误** 代码示例：



```js
/*eslint wrap-iife: ["error", "inside"]*/

var x = function () { return { y: 1 };}(); // unwrapped
var x = (function () { return { y: 1 };}()); // wrapped call expression
```

选项 `"inside"` 的 **正确** 代码示例：

::: correct

```js
/*eslint wrap-iife: ["error", "inside"]*/

var x = (function () { return { y: 1 };})(); // wrapped function expression
```

### any

选项 `"any"` 的 **错误** 代码示例：



```js
/*eslint wrap-iife: ["error", "any"]*/

var x = function () { return { y: 1 };}(); // unwrapped
```

选项 `"any"` 的 **正确** 代码示例：

::: correct

```js
/*eslint wrap-iife: ["error", "any"]*/

var x = (function () { return { y: 1 };}()); // wrapped call expression
var x = (function () { return { y: 1 };})(); // wrapped function expression
```

### functionPrototypeMethods

选项 `"inside", { "functionPrototypeMethods": true }`  的 **错误** 代码示例：



```js
/* eslint wrap-iife: [2, "inside", { functionPrototypeMethods: true }] */

var x = function(){ foo(); }()
var x = (function(){ foo(); }())
var x = function(){ foo(); }.call(bar)
var x = (function(){ foo(); }.call(bar))
```

选项 `"inside", { "functionPrototypeMethods": true }`  的 **正确** 代码示例：

::: correct

```js
/* eslint wrap-iife: [2, "inside", { functionPrototypeMethods: true }] */

var x = (function(){ foo(); })()
var x = (function(){ foo(); }).call(bar)
```
