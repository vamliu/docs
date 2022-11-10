---
规则名: no-with
规则类型: suggestion
深入了解:
- https://web.archive.org/web/20200717110117/https://yuiblog.com/blog/2006/04/11/with-statement-considered-harmful/
---



The `with` statement is potentially problematic because it adds members of an object to the current scope, making it impossible to tell what a variable inside the block actually refers to.

## 规则详解

This rule disallows `with` statements.

If ESLint parses code in strict mode, the parser (instead of this rule) reports the error.

此规则的 **错误** 代码实例：



```js
/*eslint no-with: "error"*/

with (point) {
    r = Math.sqrt(x * x + y * y); // is r a member of point?
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-with: "error"*/
/*eslint-env es6*/

const r = ({x, y}) => Math.sqrt(x * x + y * y);
```

## 禁用建议

If you intentionally use `with` statements then you can disable this rule.
