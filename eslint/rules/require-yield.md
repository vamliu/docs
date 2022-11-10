---
规则名: require-yield
规则类型: suggestion
关联规则:
- require-await
---



## 规则详解

This rule generates warnings for generator functions that do not have the `yield` keyword.

## Examples

此规则的 **错误** 代码实例：



```js
/*eslint require-yield: "error"*/
/*eslint-env es6*/

function* foo() {
  return 10;
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint require-yield: "error"*/
/*eslint-env es6*/

function* foo() {
  yield 5;
  return 10;
}

function foo() {
  return 10;
}

// This rule does not warn on empty generator functions.
function* foo() { }
```

## 禁用建议

If you don't want to notify generator functions that have no `yield` expression, then it's safe to disable this rule.
