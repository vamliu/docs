---
规则名: no-async-promise-executor
规则类型: problem
---



The `new Promise` constructor accepts an *executor* function as an argument, which has `resolve` and `reject` parameters that can be used to control the state of the created Promise. For example:

```js
const result = new Promise(function executor(resolve, reject) {
  readFile('foo.txt', function(err, result) {
    if (err) {
      reject(err);
    } else {
      resolve(result);
    }
  });
});
```

The executor function can also be an `async function`. However, this is usually a mistake, for a few reasons:

* If an async executor function throws an error, the error will be lost and won't cause the newly-constructed `Promise` to reject. This could make it difficult to debug and handle some errors.
* If a Promise executor function is using `await`, this is usually a sign that it is not actually necessary to use the `new Promise` constructor, or the scope of the `new Promise` constructor can be reduced.

## 规则详解

This rule aims to disallow async Promise executor functions.

此规则的 **错误** 代码实例：



```js
const foo = new Promise(async (resolve, reject) => {
  readFile('foo.txt', function(err, result) {
    if (err) {
      reject(err);
    } else {
      resolve(result);
    }
  });
});

const result = new Promise(async (resolve, reject) => {
  resolve(await foo);
});
```

此规则的 **正确** 代码实例：

::: correct

```js
const foo = new Promise((resolve, reject) => {
  readFile('foo.txt', function(err, result) {
    if (err) {
      reject(err);
    } else {
      resolve(result);
    }
  });
});

const result = Promise.resolve(foo);
```

## 禁用建议

If your codebase doesn't support async function syntax, there's no need to enable this rule.
