---
规则名: prefer-numeric-literals
规则类型: suggestion
---



The `parseInt()` and `Number.parseInt()` functions can be used to turn binary, octal, and hexadecimal strings into integers. As binary, octal, and hexadecimal literals are supported in ES6, this rule encourages use of those numeric literals instead of `parseInt()` or `Number.parseInt()`.

```js
0b111110111 === 503;
0o767 === 503;
```

## 规则详解

This rule disallows calls to `parseInt()` or `Number.parseInt()` if called with two arguments: a string; and a radix option of 2 (binary), 8 (octal), or 16 (hexadecimal).

此规则的 **错误** 代码实例：



```js
/*eslint prefer-numeric-literals: "error"*/

parseInt("111110111", 2) === 503;
parseInt(`111110111`, 2) === 503;
parseInt("767", 8) === 503;
parseInt("1F7", 16) === 503;
Number.parseInt("111110111", 2) === 503;
Number.parseInt("767", 8) === 503;
Number.parseInt("1F7", 16) === 503;
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint prefer-numeric-literals: "error"*/
/*eslint-env es6*/

parseInt(1);
parseInt(1, 3);
Number.parseInt(1);
Number.parseInt(1, 3);

0b111110111 === 503;
0o767 === 503;
0x1F7 === 503;

a[parseInt](1,2);

parseInt(foo);
parseInt(foo, 2);
Number.parseInt(foo);
Number.parseInt(foo, 2);
```

## 禁用建议

If you want to allow use of `parseInt()` or `Number.parseInt()` for binary, octal, or hexadecimal integers, or if you are not using ES6 (because binary and octal literals are not supported in ES5 and below), you may wish to disable this rule.

## 兼容

* **JSCS**: [requireNumericLiterals](https://jscs-dev.github.io/rule/requireNumericLiterals)
