---
规则名: no-empty-label
布局: doc

关联规则:
- no-labels
- no-label-var
- no-unused-labels
---

Disallows labels for anything other than loops and switches.

(removed) This rule was **removed** in ESLint v2.0 and **replaced** by the [no-labels](no-labels) rule.

Labeled statements are only used in conjunction with labeled break and continue statements. ECMAScript has no goto statement.

## 规则详解

This error occurs when a label is used to mark a statement that is not an iteration or switch

Example of **incorrect** code for this rule:



```js
/*eslint no-empty-label: "error"*/

labeled:
var x = 10;
```

Example of **correct** code for this rule:

::: correct

```js
/*eslint no-empty-label: "error"*/

labeled:
for (var i=10; i; i--) {
    // ...
}
```

## 使用建议

If you don't want to be notified about usage of labels, then it's safe to disable this rule.
