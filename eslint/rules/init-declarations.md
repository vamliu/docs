---
规则名: init-declarations
布局: doc
规则类型: suggestion
---


In JavaScript, variables can be assigned during declaration, or at any point afterwards using an assignment statement. For example, in the following code, `foo` is initialized during declaration, while `bar` is initialized later.

```js
var foo = 1;
var bar;

if (foo) {
    bar = 1;
} else {
    bar = 2;
}
```

## 规则详解

This rule is aimed at enforcing or eliminating variable initializations during declaration. For example, in the following code, `foo` is initialized during declaration, while `bar` is not.

```js
var foo = 1;
var bar;

bar = 2;
```

This rule aims to bring consistency to variable initializations and declarations.

## 配置项

The rule takes two options:

1. A string which must be either `"always"` (the default), to enforce initialization at declaration, or `"never"` to disallow initialization during declaration. This rule applies to `var`, `let`, and `const` variables, however `"never"` is ignored for `const` variables, as unassigned `const`s generate a parse error.
2. An object that further controls the behavior of this rule. Currently, the only available parameter is `ignoreForLoopInit`, which indicates if initialization at declaration is allowed in `for` loops when `"never"` is set, since it is a very typical use case.

You can configure the rule as follows:

Variables must be initialized at declaration (default)

```json
{
    "init-declarations": ["error", "always"],
}
```

Variables must not be initialized at declaration

```json
{
    "init-declarations": ["error", "never"]
}
```

Variables must not be initialized at declaration, except in for loops, where it is allowed

```json
{
    "init-declarations": ["error", "never", { "ignoreForLoopInit": true }]
}
```

### always

选项 default `"always"` 的 **错误** 代码示例：



```js
/*eslint init-declarations: ["error", "always"]*/
/*eslint-env es6*/

function foo() {
    var bar;
    let baz;
}
```

选项 default `"always"` 的 **正确** 代码示例：

::: correct

```js
/*eslint init-declarations: ["error", "always"]*/
/*eslint-env es6*/

function foo() {
    var bar = 1;
    let baz = 2;
    const qux = 3;
}
```

### never

选项 `"never"` 的 **错误** 代码示例：



```js
/*eslint init-declarations: ["error", "never"]*/
/*eslint-env es6*/

function foo() {
    var bar = 1;
    let baz = 2;

    for (var i = 0; i < 1; i++) {}
}
```

选项 `"never"` 的 **正确** 代码示例：

::: correct

```js
/*eslint init-declarations: ["error", "never"]*/
/*eslint-env es6*/

function foo() {
    var bar;
    let baz;
    const buzz = 1;
}
```

The `"never"` option ignores `const` variable initializations.

### ignoreForLoopInit

Examples of **correct** code for the `"never", { "ignoreForLoopInit": true }` options:

::: correct

```js
/*eslint init-declarations: ["error", "never", { "ignoreForLoopInit": true }]*/
for (var i = 0; i < 1; i++) {}
```

## 使用建议

When you are indifferent as to how your variables are initialized.
