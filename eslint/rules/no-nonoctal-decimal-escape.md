---
规则名: no-nonoctal-decimal-escape
规则类型: suggestion
关联规则:
- no-octal-escape
深入了解:
- https://tc39.es/ecma262/#prod-annexB-NonOctalDecimalEscapeSequence
---





Although not being specified in the language until ECMAScript 2021, `\8` and `\9` escape sequences in string literals were allowed in most JavaScript engines, and treated as "useless" escapes:

```js
"\8" === "8"; // true
"\9" === "9"; // true
```

Since ECMAScript 2021, these escape sequences are specified as [non-octal decimal escape sequences](https://tc39.es/ecma262/#prod-annexB-NonOctalDecimalEscapeSequence), retaining the same behavior.

Nevertheless, the ECMAScript specification treats `\8` and `\9` in string literals as a legacy feature. This syntax is optional if the ECMAScript host is not a web browser. Browsers still have to support it, but only in non-strict mode.

Regardless of your targeted environment, these escape sequences shouldn't be used when writing new code.

## 规则详解

This rule disallows `\8` and `\9` escape sequences in string literals.

此规则的 **错误** 代码实例：



```js
/*eslint no-nonoctal-decimal-escape: "error"*/

"\8";

"\9";

var foo = "w\8less";

var bar = "December 1\9";

var baz = "Don't use \8 and \9 escapes.";

var quux = "\0\8";
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-nonoctal-decimal-escape: "error"*/

"8";

"9";

var foo = "w8less";

var bar = "December 19";

var baz = "Don't use \\8 and \\9 escapes.";

var quux = "\0\u0038";
```
