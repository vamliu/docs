---
规则名: newline-before-return
规则类型: layout
关联规则:
- newline-after-var
---



This rule was **deprecated** in ESLint v4.0.0 and replaced by the [padding-line-between-statements](padding-line-between-statements) rule.

There is no hard and fast rule about whether empty lines should precede `return` statements in JavaScript. However, clearly delineating where a function is returning can greatly increase the readability and clarity of the code. For example:

```js
function foo(bar) {
  var baz = 'baz';
  if (!bar) {
    bar = baz;
    return bar;
  }
  return bar;
}
```

Adding newlines visibly separates the return statements from the previous lines, making it clear where the function exits and what value it returns:

```js
function foo(bar) {
  var baz = 'baz';

  if (!bar) {
    bar = baz;

    return bar;
  }

  return bar;
}
```

## 规则详解

This rule requires an empty line before `return` statements to increase code clarity, except when the `return` is alone inside a statement group (such as an if statement). In the latter case, the `return` statement does not need to be delineated by virtue of it being alone. Comments are ignored and do not count as empty lines.

此规则的 **错误** 代码实例：



```js
/*eslint newline-before-return: "error"*/

function foo(bar) {
    if (!bar) {
        return;
    }
    return bar;
}

function foo(bar) {
    if (!bar) {
        return;
    }
    /* multi-line
    comment */
    return bar;
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint newline-before-return: "error"*/

function foo() {
    return;
}

function foo() {

    return;
}

function foo(bar) {
    if (!bar) return;
}

function foo(bar) {
    if (!bar) { return };
}

function foo(bar) {
    if (!bar) {
        return;
    }
}

function foo(bar) {
    if (!bar) {
        return;
    }

    return bar;
}

function foo(bar) {
    if (!bar) {

        return;
    }
}

function foo() {

    // comment
    return;
}
```

## 禁用建议

You can safely disable this rule if you do not have any strict conventions about whitespace before `return` statements.
