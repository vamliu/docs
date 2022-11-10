---
规则名: func-call-spacing
规则类型: layout
关联规则:
- no-spaced-func
---



When calling a function, developers may insert optional whitespace between the function's name and the parentheses that invoke it. The following pairs of function calls are equivalent:

```js
alert('Hello');
alert ('Hello');

console.log(42);
console.log (42);

new Date();
new Date ();
```

## 规则详解

This rule requires or disallows spaces between the function name and the opening parenthesis that calls it.

## 配置项

This rule has a string option:

* `"never"` (default) disallows space between the function name and the opening parenthesis.
* `"always"` requires space between the function name and the opening parenthesis.

Further, in `"always"` mode, a second object option is available that contains a single boolean `allowNewlines` property.

### never

选项 `"never"`  默认值的 **错误** 代码示例：



```js
/*eslint func-call-spacing: ["error", "never"]*/

fn ();

fn
();
```

选项 `"never"` 默认值的 **正确** 代码示例：

::: correct

```js
/*eslint func-call-spacing: ["error", "never"]*/

fn();
```

### always

选项 `"always"` 的 **错误** 代码示例：



```js
/*eslint func-call-spacing: ["error", "always"]*/

fn();

fn
();
```

选项 `"always"` 的 **正确** 代码示例：

::: correct

```js
/*eslint func-call-spacing: ["error", "always"]*/

fn ();
```

#### allowNewlines

By default, `"always"` does not allow newlines. To permit newlines when in `"always"` mode, set the `allowNewlines` option to `true`. Newlines are never required.

Examples of **incorrect** code for this rule with `allowNewlines` option enabled:



```js
/*eslint func-call-spacing: ["error", "always", { "allowNewlines": true }]*/

fn();
```

Examples of **correct** code for this rule with the `allowNewlines` option enabled:

::: correct

```js
/*eslint func-call-spacing: ["error", "always", { "allowNewlines": true }]*/

fn (); // Newlines are never required.

fn
();
```

## 禁用建议

This rule can safely be turned off if your project does not care about enforcing a consistent style for spacing within function calls.

## 兼容

* **JSCS**: [disallowSpacesInCallExpression](https://jscs-dev.github.io/rule/disallowSpacesInCallExpression)
* **JSCS**: [requireSpacesInCallExpression](https://jscs-dev.github.io/rule/requireSpacesInCallExpression)
