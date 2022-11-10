---
规则名: no-delete-var
规则类型: suggestion
---



The purpose of the `delete` operator is to remove a property from an object. Using the `delete` operator on a variable might lead to unexpected behavior.

## 规则详解

This rule disallows the use of the `delete` operator on variables.

If ESLint parses code in strict mode, the parser (instead of this rule) reports the error.

此规则的 **错误** 代码实例：



```js
/*eslint no-delete-var: "error"*/

var x;
delete x;
```
