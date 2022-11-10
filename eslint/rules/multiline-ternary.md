---
规则名: multiline-ternary
规则类型: layout
关联规则:
- operator-linebreak
---



JavaScript allows operands of ternary expressions to be separated by newlines, which can improve the readability of your program.

For example:

```js
var foo = bar > baz ? value1 : value2;
```

The above can be rewritten as the following to improve readability and more clearly delineate the operands:

```js
var foo = bar > baz ?
    value1 :
    value2;
```

## 规则详解

This rule enforces or disallows newlines between operands of a ternary expression.
Note: The location of the operators is not enforced by this rule. Please see the [operator-linebreak](operator-linebreak) rule if you are interested in enforcing the location of the operators themselves.

## 配置项

This rule has a string option:

* `"always"` (default) enforces newlines between the operands of a ternary expression.
* `"always-multiline"` enforces newlines between the operands of a ternary expression if the expression spans multiple lines.
* `"never"` disallows newlines between the operands of a ternary expression.

### always

This is the default option.

选项 `"always"` 的 **错误** 代码示例：



```js
/*eslint multiline-ternary: ["error", "always"]*/

foo > bar ? value1 : value2;

foo > bar ? value :
    value2;

foo > bar ?
    value : value2;
```

选项 `"always"` 的 **正确** 代码示例：

::: correct

```js
/*eslint multiline-ternary: ["error", "always"]*/

foo > bar ?
    value1 :
    value2;

foo > bar ?
    (baz > qux ?
        value1 :
        value2) :
    value3;
```

### always-multiline

选项 `"always-multiline"` 的 **错误** 代码示例：



```js
/*eslint multiline-ternary: ["error", "always-multiline"]*/

foo > bar ? value1 :
    value2;

foo > bar ?
    value1 : value2;

foo > bar &&
    bar > baz ? value1 : value2;
```

选项 `"always-multiline"` 的 **正确** 代码示例：

::: correct

```js
/*eslint multiline-ternary: ["error", "always-multiline"]*/

foo > bar ? value1 : value2;

foo > bar ?
    value1 :
    value2;

foo > bar ?
    (baz > qux ? value1 : value2) :
    value3;

foo > bar ?
    (baz > qux ?
        value1 :
        value2) :
    value3;

foo > bar &&
    bar > baz ?
        value1 :
        value2;
```

### never

选项 `"never"` 的 **错误** 代码示例：



```js
/*eslint multiline-ternary: ["error", "never"]*/

foo > bar ? value :
    value2;

foo > bar ?
    value : value2;

foo >
    bar ?
    value1 :
    value2;
```

选项 `"never"` 的 **正确** 代码示例：

::: correct

```js
/*eslint multiline-ternary: ["error", "never"]*/

foo > bar ? value1 : value2;

foo > bar ? (baz > qux ? value1 : value2) : value3;

foo > bar ? (
    baz > qux ? value1 : value2
) : value3;
```

## 禁用建议

You can safely disable this rule if you do not have any strict conventions about whether the operands of a ternary expression should be separated by newlines.

## 兼容

* **JSCS**: [requireMultiLineTernary](https://jscs-dev.github.io/rule/requireMultiLineTernary)
