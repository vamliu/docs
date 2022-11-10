---
规则名: no-param-reassign
规则类型: suggestion
深入了解:
- https://spin.atomicobject.com/2011/04/10/javascript-don-t-reassign-your-function-arguments/
---


Assignment to variables declared as function parameters can be misleading and lead to confusing behavior, as modifying function parameters will also mutate the `arguments` object. Often, assignment to function parameters is unintended and indicative of a mistake or programmer error.

This rule can be also configured to fail when function parameters are modified. Side effects on parameters can cause counter-intuitive execution flow and make errors difficult to track down.

## 规则详解

This rule aims to prevent unintended behavior caused by modification or reassignment of function parameters.

此规则的 **错误** 代码实例：



```js
/*eslint no-param-reassign: "error"*/

function foo(bar) {
    bar = 13;
}

function foo(bar) {
    bar++;
}

function foo(bar) {
    for (bar in baz) {}
}

function foo(bar) {
    for (bar of baz) {}
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-param-reassign: "error"*/

function foo(bar) {
    var baz = bar;
}
```

## 配置项

This rule takes one option, an object, with a boolean property `"props"`, and  arrays `"ignorePropertyModificationsFor"` and `"ignorePropertyModificationsForRegex"`. `"props"` is `false` by default. If `"props"` is set to `true`, this rule warns against the modification of parameter properties unless they're included in `"ignorePropertyModificationsFor"` or `"ignorePropertyModificationsForRegex"`, which is an empty array by default.

### props

选项 default `{ "props": false }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-param-reassign: ["error", { "props": false }]*/

function foo(bar) {
    bar.prop = "value";
}

function foo(bar) {
    delete bar.aaa;
}

function foo(bar) {
    bar.aaa++;
}

function foo(bar) {
    for (bar.aaa in baz) {}
}

function foo(bar) {
    for (bar.aaa of baz) {}
}
```

选项 `{ "props": true }` 的 **错误** 代码示例：



```js
/*eslint no-param-reassign: ["error", { "props": true }]*/

function foo(bar) {
    bar.prop = "value";
}

function foo(bar) {
    delete bar.aaa;
}

function foo(bar) {
    bar.aaa++;
}

function foo(bar) {
    for (bar.aaa in baz) {}
}

function foo(bar) {
    for (bar.aaa of baz) {}
}
```

Examples of **correct** code for the `{ "props": true }` option with `"ignorePropertyModificationsFor"` set:

::: correct

```js
/*eslint no-param-reassign: ["error", { "props": true, "ignorePropertyModificationsFor": ["bar"] }]*/

function foo(bar) {
    bar.prop = "value";
}

function foo(bar) {
    delete bar.aaa;
}

function foo(bar) {
    bar.aaa++;
}

function foo(bar) {
    for (bar.aaa in baz) {}
}

function foo(bar) {
    for (bar.aaa of baz) {}
}
```

Examples of **correct** code for the `{ "props": true }` option with `"ignorePropertyModificationsForRegex"` set:

::: correct

```js
/*eslint no-param-reassign: ["error", { "props": true, "ignorePropertyModificationsForRegex": ["^bar"] }]*/

function foo(barVar) {
    barVar.prop = "value";
}

function foo(barrito) {
    delete barrito.aaa;
}

function foo(bar_) {
    bar_.aaa++;
}

function foo(barBaz) {
    for (barBaz.aaa in baz) {}
}

function foo(barBaz) {
    for (barBaz.aaa of baz) {}
}
```

## 禁用建议

If you want to allow assignment to function parameters, then you can safely disable this rule.
