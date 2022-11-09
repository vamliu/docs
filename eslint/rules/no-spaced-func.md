---
规则名: no-spaced-func
布局: doc
规则类型: layout
---



This rule was **deprecated** in ESLint v3.3.0 and replaced by the [func-call-spacing](func-call-spacing) rule.

While it's possible to have whitespace between the name of a function and the parentheses that execute it, such patterns tend to look more like errors.

## 规则详解

This rule disallows spacing between function identifiers and their applications.

Examples of **incorrect** code for this rule:



```js
/*eslint no-spaced-func: "error"*/

fn ()

fn
()
```

Examples of **correct** code for this rule:

::: correct

```js
/*eslint no-spaced-func: "error"*/

fn()
```
