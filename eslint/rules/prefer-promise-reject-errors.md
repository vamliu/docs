---
规则名: prefer-promise-reject-errors
规则类型: suggestion
关联规则:
- no-throw-literal
深入了解:
- http://bluebirdjs.com/docs/warning-explanations.html#warning-a-promise-was-rejected-with-a-non-error
---


It is considered good practice to only pass instances of the built-in `Error` object to the `reject()` function for user-defined errors in Promises. `Error` objects automatically store a stack trace, which can be used to debug an error by determining where it came from. If a Promise is rejected with a non-`Error` value, it can be difficult to determine where the rejection occurred.

## 规则详解

This rule aims to ensure that Promises are only rejected with `Error` objects.

## 配置项

This rule takes one optional object argument:

* `allowEmptyReject: true` (`false` by default) allows calls to `Promise.reject()` with no arguments.

此规则的 **错误** 代码实例：



```js
/*eslint prefer-promise-reject-errors: "error"*/

Promise.reject("something bad happened");

Promise.reject(5);

Promise.reject();

new Promise(function(resolve, reject) {
  reject("something bad happened");
});

new Promise(function(resolve, reject) {
  reject();
});

```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint prefer-promise-reject-errors: "error"*/

Promise.reject(new Error("something bad happened"));

Promise.reject(new TypeError("something bad happened"));

new Promise(function(resolve, reject) {
  reject(new Error("something bad happened"));
});

var foo = getUnknownValue();
Promise.reject(foo);
```

选项 `allowEmptyReject: true` 的 **正确** 代码示例：

::: correct

```js
/*eslint prefer-promise-reject-errors: ["error", {"allowEmptyReject": true}]*/

Promise.reject();

new Promise(function(resolve, reject) {
  reject();
});
```

## 已知局限

Due to the limits of static analysis, this rule cannot guarantee that you will only reject Promises with `Error` objects. While the rule will report cases where it can guarantee that the rejection reason is clearly not an `Error`, it will not report cases where there is uncertainty about whether a given reason is an `Error`. For more information on this caveat, see the [similar limitations](no-throw-literal#known-limitations) in the `no-throw-literal` rule.

To avoid conflicts between rules, this rule does not report non-error values used in `throw` statements in async functions, even though these lead to Promise rejections. To lint for these cases, use the [`no-throw-literal`](no-throw-literal) rule.

## 禁用建议

If you're using custom non-error values as Promise rejection reasons, you can turn off this rule.
