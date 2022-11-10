---
规则名: no-bitwise
规则类型: suggestion
---


The use of bitwise operators in JavaScript is very rare and often `&` or `|` is simply a mistyped `&&` or `||`, which will lead to unexpected behavior.

```js
var x = y | z;
```

## 规则详解

This rule disallows bitwise operators.

此规则的 **错误** 代码实例：



```js
/*eslint no-bitwise: "error"*/

var x = y | z;

var x = y & z;

var x = y ^ z;

var x = ~ z;

var x = y << z;

var x = y >> z;

var x = y >>> z;

x |= y;

x &= y;

x ^= y;

x <<= y;

x >>= y;

x >>>= y;
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-bitwise: "error"*/

var x = y || z;

var x = y && z;

var x = y > z;

var x = y < z;

x += y;
```

## 配置项

This rule has an object option:

* `"allow"`: Allows a list of bitwise operators to be used as exceptions.
* `"int32Hint"`: Allows the use of bitwise OR in `|0` pattern for type casting.

### allow

选项 `{ "allow": ["~"] }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-bitwise: ["error", { "allow": ["~"] }] */

~[1,2,3].indexOf(1) === -1;
```

### int32Hint

选项 `{ "int32Hint": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-bitwise: ["error", { "int32Hint": true }] */

var b = a|0;
```
