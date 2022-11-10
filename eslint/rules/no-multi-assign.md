---
规则名: no-multi-assign
规则类型: suggestion
关联规则:
- max-statements-per-line
---


Chaining the assignment of variables can lead to unexpected results and be difficult to read.

```js
(function() {
    const foo = bar = 0; // Did you mean `foo = bar == 0`?
    bar = 1;             // This will not fail since `bar` is not constant.
})();
console.log(bar);        // This will output 1 since `bar` is not scoped.
```

## 规则详解

This rule disallows using multiple assignments within a single statement.

此规则的 **错误** 代码实例：



```js
/*eslint no-multi-assign: "error"*/

var a = b = c = 5;

const foo = bar = "baz";

let a =
    b =
    c;

class Foo {
    a = b = 10;
}

a = b = "quux";
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-multi-assign: "error"*/

var a = 5;
var b = 5;
var c = 5;

const foo = "baz";
const bar = "baz";

let a = c;
let b = c;

class Foo {
    a = 10;
    b = 10;
}

a = "quux";
b = "quux";
```

## 配置项

This rule has an object option:

* `"ignoreNonDeclaration"`: When set to `true`, the rule allows chains that don't include initializing a variable in a declaration or initializing a class field. Default is `false`.

### ignoreNonDeclaration

选项 `{ "ignoreNonDeclaration": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-multi-assign: ["error", { "ignoreNonDeclaration": true }]*/

let a;
let b;
a = b = "baz";

const x = {};
const y = {};
x.one = y.one = 1;
```

选项 `{ "ignoreNonDeclaration": true }` 的 **错误** 代码示例：



```js
/*eslint no-multi-assign: ["error", { "ignoreNonDeclaration": true }]*/

let a = b = "baz";

const foo = bar = 1;

class Foo {
    a = b = 10;
}
```
