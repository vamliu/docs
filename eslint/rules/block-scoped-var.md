---
规则名: block-scoped-var
规则类型: suggestion
深入了解:
- https://www.adequatelygood.com/JavaScript-Scoping-and-Hoisting.html
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var#var_hoisting
---


The `block-scoped-var` rule generates warnings when variables are used outside of the block in which they were defined. This emulates C-style block scope.

## 规则详解

This rule aims to reduce the usage of variables outside of their binding context and emulate traditional block scope from other languages. This is to help newcomers to the language avoid difficult bugs with variable hoisting.

此规则的 **错误** 代码实例：

```js
/*eslint block-scoped-var: "error"*/

function doIf() {
    if (true) {
        var build = true;
    }

    console.log(build);
}

function doIfElse() {
    if (true) {
        var build = true;
    } else {
        var build = false;
    }
}

function doTryCatch() {
    try {
        var build = 1;
    } catch (e) {
        var f = build;
    }
}

function doFor() {
    for (var x = 1; x < 10; x++) {
        var y = f(x);
    }
    console.log(y);
}

class C {
    static {
        if (something) {
            var build = true;
        }
        build = false;
    }
}
```

此规则的 **正确** 代码实例：

```js
/*eslint block-scoped-var: "error"*/

function doIf() {
    var build;

    if (true) {
        build = true;
    }

    console.log(build);
}

function doIfElse() {
    var build;

    if (true) {
        build = true;
    } else {
        build = false;
    }
}

function doTryCatch() {
    var build;
    var f;

    try {
        build = 1;
    } catch (e) {
        f = build;
    }
}

function doFor() {
    for (var x = 1; x < 10; x++) {
        var y = f(x);
        console.log(y);
    }
}

class C {
    static {
        var build = false;
        if (something) {
            build = true;
        }
    }
}
```
