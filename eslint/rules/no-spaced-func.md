---
规则名: no-spaced-func
规则类型: layout
---



This rule was **deprecated** in ESLint v3.3.0 and replaced by the [func-call-spacing](func-call-spacing) rule.

While it's possible to have whitespace between the name of a function and the parentheses that execute it, such patterns tend to look more like errors.

## 规则详解

This rule disallows spacing between function identifiers and their applications.

此规则的 **错误** 代码实例：



```js
/*eslint no-spaced-func: "error"*/

fn ()

fn
()
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-spaced-func: "error"*/

fn()
```
