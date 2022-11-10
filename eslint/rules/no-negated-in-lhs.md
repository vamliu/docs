---
规则名: no-negated-in-lhs
规则类型: problem
---


This rule was **deprecated** in ESLint v3.3.0 and replaced by the [no-unsafe-negation](no-unsafe-negation) rule.

Just as developers might type `-a + b` when they mean `-(a + b)` for the negative of a sum, they might type `!key in object` by mistake when they almost certainly mean `!(key in object)` to test that a key is not in an object.

## 规则详解

This rule disallows negating the left operand in `in` expressions.

此规则的 **错误** 代码实例：



```js
/*eslint no-negated-in-lhs: "error"*/

if(!key in object) {
    // operator precedence makes it equivalent to (!key) in object
    // and type conversion makes it equivalent to (key ? "false" : "true") in object
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-negated-in-lhs: "error"*/

if(!(key in object)) {
    // key is not in object
}

if(('' + !key) in object) {
    // make operator precedence and type conversion explicit
    // in a rare situation when that is the intended meaning
}
```

## 禁用建议

Never.
