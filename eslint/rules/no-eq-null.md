---
规则名: no-eq-null
规则类型: suggestion
---


Comparing to `null` without a type-checking operator (`==` or `!=`), can have unintended results as the comparison will evaluate to true when comparing to not just a `null`, but also an `undefined` value.

```js
if (foo == null) {
  bar();
}
```

## 规则详解

The `no-eq-null` rule aims reduce potential bug and unwanted behavior by ensuring that comparisons to `null` only match `null`, and not also `undefined`. As such it will flag comparisons to null when using `==` and `!=`.

此规则的 **错误** 代码实例：



```js
/*eslint no-eq-null: "error"*/

if (foo == null) {
  bar();
}

while (qux != null) {
  baz();
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-eq-null: "error"*/

if (foo === null) {
  bar();
}

while (qux !== null) {
  baz();
}
```

## 禁用建议

If you want to enforce type-checking operations in general, use the more powerful [eqeqeq](./eqeqeq) instead.

## 兼容

* **JSHint**: This rule corresponds to `eqnull` rule of JSHint.
