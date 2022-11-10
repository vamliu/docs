---
规则名: no-else-return
规则类型: suggestion
---



If an `if` block contains a `return` statement, the `else` block becomes unnecessary. Its contents can be placed outside of the block.

```js
function foo() {
    if (x) {
        return y;
    } else {
        return z;
    }
}
```

## 规则详解

This rule is aimed at highlighting an unnecessary block of code following an `if` containing a return statement. As such, it will warn when it encounters an `else` following a chain of `if`s, all of them containing a `return` statement.

## 配置项

This rule has an object option:

* `allowElseIf: true` (default) allows `else if` blocks after a return
* `allowElseIf: false` disallows `else if` blocks after a return

### `allowElseIf: true`

此规则的 **错误** 代码实例：



```js
/*eslint no-else-return: "error"*/

function foo() {
    if (x) {
        return y;
    } else {
        return z;
    }
}

function foo() {
    if (x) {
        return y;
    } else if (z) {
        return w;
    } else {
        return t;
    }
}

function foo() {
    if (x) {
        return y;
    } else {
        var t = "foo";
    }

    return t;
}

function foo() {
    if (error) {
        return 'It failed';
    } else {
        if (loading) {
            return "It's still loading";
        }
    }
}

// Two warnings for nested occurrences
function foo() {
    if (x) {
        if (y) {
            return y;
        } else {
            return x;
        }
    } else {
        return z;
    }
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-else-return: "error"*/

function foo() {
    if (x) {
        return y;
    }

    return z;
}

function foo() {
    if (x) {
        return y;
    } else if (z) {
        var t = "foo";
    } else {
        return w;
    }
}

function foo() {
    if (x) {
        if (z) {
            return y;
        }
    } else {
        return z;
    }
}

function foo() {
    if (error) {
        return 'It failed';
    } else if (loading) {
        return "It's still loading";
    }
}
```

### `allowElseIf: false`

此规则的 **错误** 代码实例：



```js
/*eslint no-else-return: ["error", {allowElseIf: false}]*/

function foo() {
    if (error) {
        return 'It failed';
    } else if (loading) {
        return "It's still loading";
    }
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-else-return: ["error", {allowElseIf: false}]*/

function foo() {
    if (error) {
        return 'It failed';
    }

    if (loading) {
        return "It's still loading";
    }
}
```
