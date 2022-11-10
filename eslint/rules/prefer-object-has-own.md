---
规则名: prefer-object-has-own
规则类型: suggestion
深入了解:
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwn
---



It is very common to write code like:

```js
if (Object.prototype.hasOwnProperty.call(object, "foo")) {
  console.log("has property foo");
}
```

This is a common practice because methods on `Object.prototype` can sometimes be unavailable or redefined (see the [no-prototype-builtins](no-prototype-builtins) rule).

Introduced in ES2022, `Object.hasOwn()` is a shorter alternative to `Object.prototype.hasOwnProperty.call()`:

```js
if (Object.hasOwn(object, "foo")) {
  console.log("has property foo")
}
```

## 规则详解

此规则的 **错误** 代码实例：



```js
/*eslint prefer-object-has-own: "error"*/

Object.prototype.hasOwnProperty.call(obj, "a");

Object.hasOwnProperty.call(obj, "a");

({}).hasOwnProperty.call(obj, "a");

const hasProperty = Object.prototype.hasOwnProperty.call(object, property);
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint prefer-object-has-own: "error"*/

Object.hasOwn(obj, "a");

const hasProperty = Object.hasOwn(object, property);
```

## 禁用建议

This rule should not be used unless ES2022 is supported in your codebase.
