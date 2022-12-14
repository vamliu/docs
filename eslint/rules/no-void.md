---
规则名: no-void
规则类型: suggestion
关联规则:
- no-undef-init
- no-undefined
深入了解:
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/void
- https://oreilly.com/javascript/excerpts/javascript-good-parts/bad-parts.html
---


The `void` operator takes an operand and returns `undefined`: `void expression` will evaluate `expression` and return `undefined`. It can be used to ignore any side effects `expression` may produce:

The common case of using `void` operator is to get a "pure" `undefined` value as prior to ES5 the `undefined` variable was mutable:

```js
// will always return undefined
(function(){
    return void 0;
})();

// will return 1 in ES3 and undefined in ES5+
(function(){
    undefined = 1;
    return undefined;
})();

// will throw TypeError in ES5+
(function(){
    'use strict';
    undefined = 1;
})();
```

Another common case is to minify code as `void 0` is shorter than `undefined`:

```js
foo = void 0;
foo = undefined;
```

When used with IIFE (immediately-invoked function expression), `void` can be used to force the function keyword to be treated as an expression instead of a declaration:

```js
var foo = 1;
void function(){ foo = 1; }() // will assign foo a value of 1
+function(){ foo = 1; }() // same as above
```

```js
function(){ foo = 1; }() // will throw SyntaxError
```

Some code styles prohibit `void` operator, marking it as non-obvious and hard to read.

## 规则详解

This rule aims to eliminate use of void operator.

此规则的 **错误** 代码实例：



```js
/*eslint no-void: "error"*/

void foo
void someFunction();

var foo = void bar();
function baz() {
    return void 0;
}
```

## 配置项

This rule has an object option:

* `allowAsStatement` set to `true` allows the void operator to be used as a statement (Default `false`).

### allowAsStatement

When `allowAsStatement` is set to true, the rule will not error on cases that the void operator is used as a statement, i.e. when it's not used in an expression position, like in a variable assignment or a function return.

`{ "allowAsStatement": true }` 的 **错误** 代码示例：



```js
/*eslint no-void: ["error", { "allowAsStatement": true }]*/

var foo = void bar();
function baz() {
    return void 0;
}
```

`{ "allowAsStatement": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-void: ["error", { "allowAsStatement": true }]*/

void foo;
void someFunction();
```

## 禁用建议

If you intentionally use the `void` operator then you can disable this rule.
