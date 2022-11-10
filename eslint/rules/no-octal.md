---
规则名: no-octal
规则类型: suggestion
---



Octal literals are numerals that begin with a leading zero, such as:

```js
var num = 071;      // 57
```

Because the leading zero which identifies an octal literal has been a source of confusion and error in JavaScript code, ECMAScript 5 deprecates the use of octal numeric literals.

## 规则详解

The rule disallows octal literals.

If ESLint parses code in strict mode, the parser (instead of this rule) reports the error.

此规则的 **错误** 代码实例：



```js
/*eslint no-octal: "error"*/

var num = 071;
var result = 5 + 07;
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-octal: "error"*/

var num  = "071";
```

## 兼容

* **JSHint**: W115
