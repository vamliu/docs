---
规则名: space-after-function-name

---

Enforces consistent spacing after name in function definitions.

(removed) This rule was **removed** in ESLint v1.0 and **replaced** by the [space-before-function-paren](space-before-function-paren) rule.

Whitespace between a function name and its parameter list is optional.

```js
function withoutSpace(x) {
    // ...
}

function withSpace (x) {
    // ...
}
```

Some style guides may require a consistent spacing for function names.

## 规则详解

This rule aims to enforce a consistent spacing after function names. It takes one argument. If it is `"always"` then all function names must be followed by at least one space. If `"never"` then there should be no spaces between the name and the parameter list. The default is `"never"`.

此规则的 **错误** 代码实例：



```js
function foo (x) {
    // ...
}

var x = function named (x) {};

// When ["error", "always"]
function bar(x) {
    // ...
}
```

此规则的 **正确** 代码实例：

::: correct

```js
function foo(x) {
    // ...
}

var x = function named(x) {};

// When ["error", "always"]
function bar (x) {
    // ...
}
```
