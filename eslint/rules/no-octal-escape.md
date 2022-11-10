---
规则名: no-octal-escape
规则类型: suggestion
---


As of the ECMAScript 5 specification, octal escape sequences in string literals are deprecated and should not be used. Unicode escape sequences should be used instead.

```js
var foo = "Copyright \251";
```

## 规则详解

This rule disallows octal escape sequences in string literals.

If ESLint parses code in strict mode, the parser (instead of this rule) reports the error.

此规则的 **错误** 代码实例：



```js
/*eslint no-octal-escape: "error"*/

var foo = "Copyright \251";
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-octal-escape: "error"*/

var foo = "Copyright \u00A9";   // unicode

var foo = "Copyright \xA9";     // hexadecimal
```
