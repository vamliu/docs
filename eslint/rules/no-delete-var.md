---
规则名: no-delete-var
布局: doc
规则类型: suggestion
---



The purpose of the `delete` operator is to remove a property from an object. Using the `delete` operator on a variable might lead to unexpected behavior.

## 规则详解

This rule disallows the use of the `delete` operator on variables.

If ESLint parses code in strict mode, the parser (instead of this rule) reports the error.

Examples of **incorrect** code for this rule:



```js
/*eslint no-delete-var: "error"*/

var x;
delete x;
```
