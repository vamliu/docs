---
规则名: operator-assignment
规则类型: suggestion
---



JavaScript provides shorthand operators that combine variable assignment and some simple mathematical operations. For example, `x = x + 4` can be shortened to `x += 4`. The supported shorthand forms are as follows:

```text
 Shorthand | Separate
-----------|------------
 x += y    | x = x + y
 x -= y    | x = x - y
 x *= y    | x = x * y
 x /= y    | x = x / y
 x %= y    | x = x % y
 x **= y   | x = x ** y
 x <<= y   | x = x << y
 x >>= y   | x = x >> y
 x >>>= y  | x = x >>> y
 x &= y    | x = x & y
 x ^= y    | x = x ^ y
 x |= y    | x = x | y
```

## 规则详解

This rule requires or disallows assignment operator shorthand where possible.

The rule applies to the operators listed in the above table. It does not report the logical assignment operators `&&=`, `||=`, and `??=` because their short-circuiting behavior is different from the other assignment operators.

## 配置项

This rule has a single string option:

* `"always"` (default)  requires assignment operator shorthand where possible
* `"never"` disallows assignment operator shorthand

### always

选项 `"always"`  默认值的 **错误** 代码示例：



```js
/*eslint operator-assignment: ["error", "always"]*/

x = x + y;
x = y * x;
x[0] = x[0] / y;
x.y = x.y << z;
```

选项 `"always"` 默认值的 **正确** 代码示例：

::: correct

```js
/*eslint operator-assignment: ["error", "always"]*/

x = y;
x += y;
x = y * z;
x = (x * y) * z;
x[0] /= y;
x[foo()] = x[foo()] % 2;
x = y + x; // `+` is not always commutative (e.g. x = "abc")
```

### never

选项 `"never"` 的 **错误** 代码示例：



```js
/*eslint operator-assignment: ["error", "never"]*/

x *= y;
x ^= (y + z) / foo();
```

选项 `"never"` 的 **正确** 代码示例：

::: correct

```js
/*eslint operator-assignment: ["error", "never"]*/

x = x + y;
x.y = x.y / a.b;
```

## 禁用建议

Use of operator assignment shorthand is a stylistic choice. Leaving this rule turned off would allow developers to choose which style is more readable on a case-by-case basis.
