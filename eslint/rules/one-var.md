---
规则名: one-var
规则类型: suggestion
---



Variables can be declared at any point in JavaScript code using `var`, `let`, or `const`. There are many styles and preferences related to the declaration of variables, and one of those is deciding on how many variable declarations should be allowed in a single function.

There are two schools of thought in this regard:

1. There should be just one variable declaration for all variables in the function. That declaration typically appears at the top of the function.
1. You should use one variable declaration for each variable you want to define.

For instance:

```js
// one variable declaration per function
function foo() {
    var bar, baz;
}

// multiple variable declarations per function
function foo() {
    var bar;
    var baz;
}
```

The single-declaration school of thought is based in pre-ECMAScript 6 behaviors, where there was no such thing as block scope, only function scope. Since all `var` statements are hoisted to the top of the function anyway, some believe that declaring all variables in a single declaration at the top of the function removes confusion around scoping rules.

## 规则详解

This rule enforces variables to be declared either together or separately per function ( for `var`) or block (for `let` and `const`) scope.

## 配置项

This rule has one option, which can be a string option or an object option.

String option:

* `"always"` (default) requires one variable declaration per scope
* `"never"` requires multiple variable declarations per scope
* `"consecutive"` allows multiple variable declarations per scope but requires consecutive variable declarations to be combined into a single declaration

Object option:

* `"var": "always"` requires one `var` declaration per function
* `"var": "never"` requires multiple `var` declarations per function
* `"var": "consecutive"` requires consecutive `var` declarations to be a single declaration
* `"let": "always"` requires one `let` declaration per block
* `"let": "never"` requires multiple `let` declarations per block
* `"let": "consecutive"` requires consecutive `let` declarations to be a single declaration
* `"const": "always"` requires one `const` declaration per block
* `"const": "never"` requires multiple `const` declarations per block
* `"const": "consecutive"` requires consecutive `const` declarations to be a single declaration
* `"separateRequires": true` enforces `requires` to be separate from declarations

Alternate object option:

* `"initialized": "always"` requires one variable declaration for initialized variables per scope
* `"initialized": "never"` requires multiple variable declarations for initialized variables per scope
* `"initialized": "consecutive"` requires consecutive variable declarations for initialized variables to be a single declaration
* `"uninitialized": "always"` requires one variable declaration for uninitialized variables per scope
* `"uninitialized": "never"` requires multiple variable declarations for uninitialized variables per scope
* `"uninitialized": "consecutive"` requires consecutive variable declarations for uninitialized variables to be a single declaration

### always

选项 `"always"`  默认值的 **错误** 代码示例：



```js
/*eslint one-var: ["error", "always"]*/

function foo() {
    var bar;
    var baz;
    let qux;
    let norf;
}

function foo(){
    const bar = false;
    const baz = true;
    let qux;
    let norf;
}

function foo() {
    var bar;

    if (baz) {
        var qux = true;
    }
}

class C {
    static {
        var foo;
        var bar;
    }

    static {
        var foo;
        if (bar) {
            var baz = true;
        }
    }

    static {
        let foo;
        let bar;
    }
}
```

选项 `"always"` 默认值的 **正确** 代码示例：

::: correct

```js
/*eslint one-var: ["error", "always"]*/

function foo() {
    var bar,
        baz;
    let qux,
        norf;
}

function foo(){
    const bar = true,
        baz = false;
    let qux,
        norf;
}

function foo() {
    var bar,
        qux;

    if (baz) {
        qux = true;
    }
}

function foo(){
    let bar;

    if (baz) {
        let qux;
    }
}

class C {
    static {
        var foo, bar;
    }

    static {
        var foo, baz;
        if (bar) {
            baz = true;
        }
    }

    static {
        let foo, bar;
    }

    static {
        let foo;
        if (bar) {
            let baz;
        }
    }
}
```

### never

选项 `"never"` 的 **错误** 代码示例：



```js
/*eslint one-var: ["error", "never"]*/

function foo() {
    var bar,
        baz;
    const bar = true,
        baz = false;
}

function foo() {
    var bar,
        qux;

    if (baz) {
        qux = true;
    }
}

function foo(){
    let bar = true,
        baz = false;
}

class C {
    static {
        var foo, bar;
        let baz, qux;
    }
}
```

选项 `"never"` 的 **正确** 代码示例：

::: correct

```js
/*eslint one-var: ["error", "never"]*/

function foo() {
    var bar;
    var baz;
}

function foo() {
    var bar;

    if (baz) {
        var qux = true;
    }
}

function foo() {
    let bar;

    if (baz) {
        let qux = true;
    }
}

class C {
    static {
        var foo;
        var bar;
        let baz;
        let qux;
    }
}

// declarations with multiple variables are allowed in for-loop initializers
for (var i = 0, len = arr.length; i < len; i++) {
    doSomething(arr[i]);
}
```

### consecutive

选项 `"consecutive"` 的 **错误** 代码示例：



```js
/*eslint one-var: ["error", "consecutive"]*/

function foo() {
    var bar;
    var baz;
}

function foo(){
    var bar = 1;
    var baz = 2;

    qux();

    var qux = 3;
    var quux;
}

class C {
    static {
        var foo;
        var bar;
        let baz;
        let qux;
    }
}
```

选项 `"consecutive"` 的 **正确** 代码示例：

::: correct

```js
/*eslint one-var: ["error", "consecutive"]*/

function foo() {
    var bar,
        baz;
}

function foo(){
    var bar = 1,
        baz = 2;

    qux();

    var qux = 3,
        quux;
}

class C {
    static {
        var foo, bar;
        let baz, qux;
        doSomething();
        let quux;
        var quuux;
    }
}
```

### var, let, and const

选项 `{ var: "always", let: "never", const: "never" }` 的 **错误** 代码示例：



```js
/*eslint one-var: ["error", { var: "always", let: "never", const: "never" }]*/
/*eslint-env es6*/

function foo() {
    var bar;
    var baz;
    let qux,
        norf;
}

function foo() {
    const bar = 1,
          baz = 2;
    let qux,
        norf;
}
```

选项 `{ var: "always", let: "never", const: "never" }` 的 **正确** 代码示例：

::: correct

```js
/*eslint one-var: ["error", { var: "always", let: "never", const: "never" }]*/
/*eslint-env es6*/

function foo() {
    var bar,
        baz;
    let qux;
    let norf;
}

function foo() {
    const bar = 1;
    const baz = 2;
    let qux;
    let norf;
}
```

选项 `{ var: "never" }` 的 **错误** 代码示例：



```js
/*eslint one-var: ["error", { var: "never" }]*/
/*eslint-env es6*/

function foo() {
    var bar,
        baz;
}
```

选项 `{ var: "never" }` 的 **正确** 代码示例：

::: correct

```js
/*eslint one-var: ["error", { var: "never" }]*/
/*eslint-env es6*/

function foo() {
    var bar,
        baz;
    const bar = 1; // `const` and `let` declarations are ignored if they are not specified
    const baz = 2;
    let qux;
    let norf;
}
```

选项 `{ separateRequires: true }` 的 **错误** 代码示例：



```js
/*eslint one-var: ["error", { separateRequires: true, var: "always" }]*/
/*eslint-env node*/

var foo = require("foo"),
    bar = "bar";
```

选项 `{ separateRequires: true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint one-var: ["error", { separateRequires: true, var: "always" }]*/
/*eslint-env node*/

var foo = require("foo");
var bar = "bar";
```

::: correct

```js
var foo = require("foo"),
    bar = require("bar");
```

选项 `{ var: "never", let: "consecutive", const: "consecutive" }` 的 **错误** 代码示例：



```js
/*eslint one-var: ["error", { var: "never", let: "consecutive", const: "consecutive" }]*/
/*eslint-env es6*/

function foo() {
    let a,
        b;
    let c;

    var d,
        e;
}

function foo() {
    const a = 1,
        b = 2;
    const c = 3;

    var d,
        e;
}
```

选项 `{ var: "never", let: "consecutive", const: "consecutive" }` 的 **正确** 代码示例：

::: correct

```js
/*eslint one-var: ["error", { var: "never", let: "consecutive", const: "consecutive" }]*/
/*eslint-env es6*/

function foo() {
    let a,
        b;

    var d;
    var e;

    let f;
}

function foo() {
    const a = 1,
          b = 2;

    var c;
    var d;

    const e = 3;
}
```

选项 `{ var: "consecutive" }` 的 **错误** 代码示例：



```js
/*eslint one-var: ["error", { var: "consecutive" }]*/
/*eslint-env es6*/

function foo() {
    var a;
    var b;
}
```

选项 `{ var: "consecutive" }` 的 **正确** 代码示例：

::: correct

```js
/*eslint one-var: ["error", { var: "consecutive" }]*/
/*eslint-env es6*/

function foo() {
    var a,
        b;
    const c = 1; // `const` and `let` declarations are ignored if they are not specified
    const d = 2;
    let e;
    let f;
}
```

### initialized and uninitialized

选项 `{ "initialized": "always", "uninitialized": "never" }` 的 **错误** 代码示例：



```js
/*eslint one-var: ["error", { "initialized": "always", "uninitialized": "never" }]*/
/*eslint-env es6*/

function foo() {
    var a, b, c;
    var foo = true;
    var bar = false;
}
```

选项 `{ "initialized": "always", "uninitialized": "never" }` 的 **正确** 代码示例：

::: correct

```js
/*eslint one-var: ["error", { "initialized": "always", "uninitialized": "never" }]*/

function foo() {
    var a;
    var b;
    var c;
    var foo = true,
        bar = false;
}

for (let z of foo) {
    doSomething(z);
}

let z;
for (z of foo) {
    doSomething(z);
}
```

选项 `{ "initialized": "never" }` 的 **错误** 代码示例：



```js
/*eslint one-var: ["error", { "initialized": "never" }]*/
/*eslint-env es6*/

function foo() {
    var foo = true,
        bar = false;
}
```

选项 `{ "initialized": "never" }` 的 **正确** 代码示例：

::: correct

```js
/*eslint one-var: ["error", { "initialized": "never" }]*/

function foo() {
    var foo = true;
    var bar = false;
    var a, b, c; // Uninitialized variables are ignored
}
```

选项 `{ "initialized": "consecutive", "uninitialized": "never" }` 的 **错误** 代码示例：



```js
/*eslint one-var: ["error", { "initialized": "consecutive", "uninitialized": "never" }]*/

function foo() {
    var a = 1;
    var b = 2;
    var c,
        d;
    var e = 3;
    var f = 4;
}
```

选项 `{ "initialized": "consecutive", "uninitialized": "never" }` 的 **正确** 代码示例：

::: correct

```js
/*eslint one-var: ["error", { "initialized": "consecutive", "uninitialized": "never" }]*/

function foo() {
    var a = 1,
        b = 2;
    var c;
    var d;
    var e = 3,
        f = 4;
}
```

选项 `{ "initialized": "consecutive" }` 的 **错误** 代码示例：



```js
/*eslint one-var: ["error", { "initialized": "consecutive" }]*/

function foo() {
    var a = 1;
    var b = 2;

    foo();

    var c = 3;
    var d = 4;
}
```

选项 `{ "initialized": "consecutive" }` 的 **正确** 代码示例：

::: correct

```js
/*eslint one-var: ["error", { "initialized": "consecutive" }]*/

function foo() {
    var a = 1,
        b = 2;

    foo();

    var c = 3,
        d = 4;
}
```

## 兼容

* **JSHint**: This rule maps to the `onevar` JSHint rule, but allows `let` and `const` to be configured separately.
* **JSCS**: This rule roughly maps to [disallowMultipleVarDecl](https://jscs-dev.github.io/rule/disallowMultipleVarDecl).
* **JSCS**: This rule option `separateRequires` roughly maps to [requireMultipleVarDecl](https://jscs-dev.github.io/rule/requireMultipleVarDecl).
