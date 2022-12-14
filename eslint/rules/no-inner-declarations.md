---
规则名: no-inner-declarations
规则类型: problem
---



In JavaScript, prior to ES6, a function declaration is only allowed in the first level of a program or the body of another function, though parsers sometimes [erroneously accept them elsewhere](https://code.google.com/p/esprima/issues/detail?id=422). This only applies to function declarations; named or anonymous function expressions can occur anywhere an expression is permitted.

```js
// 正确
function doSomething() { }

// 错误
if (test) {
    function doSomethingElse () { }
}

function anotherThing() {
    var fn;

    if (test) {

        // 正确
        fn = function expression() { };

        // 错误
        function declaration() { }
    }
}
```

A variable declaration is permitted anywhere a statement can go, even nested deeply inside other blocks. This is often undesirable due to variable hoisting, and moving declarations to the root of the program or function body can increase clarity. Note that [block bindings](https://leanpub.com/understandinges6/read#leanpub-auto-block-bindings) (`let`, `const`) are not hoisted and therefore they are not affected by this rule.

```js
/*eslint-env es6*/

// 正确
var foo = 42;

// 正确
if (foo) {
    let bar1;
}

// 错误
while (test) {
    var bar2;
}

function doSomething() {
    // 正确
    var baz = true;

    // 错误
    if (baz) {
        var quux;
    }
}
```

## 规则详解

This rule requires that function declarations and, optionally, variable declarations be in the root of a program, or in the root of the body of a function, or in the root of the body of a class static block.

## 配置项

This rule has a string option:

* `"functions"` (default) disallows `function` declarations in nested blocks
* `"both"` disallows `function` and `var` declarations in nested blocks

### functions

选项 `"functions"`  默认值的 **错误** 代码示例：



```js
/*eslint no-inner-declarations: "error"*/

if (test) {
    function doSomething() { }
}

function doSomethingElse() {
    if (test) {
        function doAnotherThing() { }
    }
}

if (foo) function f(){}

class C {
    static {
        if (test) {
            function doSomething() { }
        }
    }
}
```

选项 `"functions"` 默认值的 **正确** 代码示例：

::: correct

```js
/*eslint no-inner-declarations: "error"*/

function doSomething() { }

function doSomethingElse() {
    function doAnotherThing() { }
}

class C {
    static {
        function doSomething() { }
    }
}

if (test) {
    asyncCall(id, function (err, data) { });
}

var fn;
if (test) {
    fn = function fnExpression() { };
}

if (foo) var a;
```

### both

选项 `"both"` 的 **错误** 代码示例：



```js
/*eslint no-inner-declarations: ["error", "both"]*/

if (test) {
    var foo = 42;
}

function doAnotherThing() {
    if (test) {
        var bar = 81;
    }
}

if (foo) var a;

if (foo) function f(){}

class C {
    static {
        if (test) {
            var something;
        }
    }
}
```

选项 `"both"` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-inner-declarations: ["error", "both"]*/

var bar = 42;

if (test) {
    let baz = 43;
}

function doAnotherThing() {
    var baz = 81;
}

class C {
    static {
        var something;
    }
}
```

## 禁用建议

The function declaration portion rule will be rendered obsolete when [block-scoped functions](https://bugzilla.mozilla.org/show_bug.cgi?id=585536) land in ES6, but until then, it should be left on to enforce valid constructions. Disable checking variable declarations when using [block-scoped-var](block-scoped-var) or if declaring variables in nested blocks is acceptable despite hoisting.
