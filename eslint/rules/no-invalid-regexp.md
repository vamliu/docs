---
规则名: no-invalid-regexp
规则类型: problem
深入了解:
- https://es5.github.io/#x7.8.5
---



An invalid pattern in a regular expression literal is a `SyntaxError` when the code is parsed, but an invalid string in `RegExp` constructors throws a `SyntaxError` only when the code is executed.

## 规则详解

This rule disallows invalid regular expression strings in `RegExp` constructors.

此规则的 **错误** 代码实例：



```js
/*eslint no-invalid-regexp: "error"*/

RegExp('[')

RegExp('.', 'z')

new RegExp('\\')
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-invalid-regexp: "error"*/

RegExp('.')

new RegExp

this.RegExp('[')
```

Please note that this rule validates regular expressions per the latest ECMAScript specification, regardless of your parser settings.

If you want to allow additional constructor flags for any reason, you can specify them using the `allowConstructorFlags` option. These flags will then be ignored by the rule.

## 配置项

This rule has an object option for exceptions:

* `"allowConstructorFlags"` is an array of flags

### allowConstructorFlags

选项 `{ "allowConstructorFlags": ["a", "z"] }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-invalid-regexp: ["error", { "allowConstructorFlags": ["a", "z"] }]*/

new RegExp('.', 'a')

new RegExp('.', 'az')
```
