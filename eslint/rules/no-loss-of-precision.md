---
规则名: no-loss-of-precision
规则类型: problem
---



This rule would disallow the use of number literals that lose precision at runtime when converted to a JS `Number` due to 64-bit floating-point rounding.

## 规则详解

In JS, `Number`s are stored as double-precision floating-point numbers according to the [IEEE 754 standard](https://en.wikipedia.org/wiki/IEEE_754). Because of this, numbers can only retain accuracy up to a certain amount of digits. If the programmer enters additional digits, those digits will be lost in the conversion to the `Number` type and will result in unexpected behavior.

此规则的 **错误** 代码实例：



```js
/*eslint no-loss-of-precision: "error"*/

const x = 9007199254740993
const x = 5123000000000000000000000000001
const x = 1230000000000000000000000.0
const x = .1230000000000000000000000
const x = 0X20000000000001
const x = 0X2_000000000_0001;
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-loss-of-precision: "error"*/

const x = 12345
const x = 123.456
const x = 123e34
const x = 12300000000000000000000000
const x = 0x1FFFFFFFFFFFFF
const x = 9007199254740991
const x = 9007_1992547409_91
```
