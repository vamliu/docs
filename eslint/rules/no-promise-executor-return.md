---
规则名: no-promise-executor-return
规则类型: problem
关联规则:
- no-async-promise-executor
深入了解:
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
---


The `new Promise` constructor accepts a single argument, called an *executor*.

```js
const myPromise = new Promise(function executor(resolve, reject) {
    readFile('foo.txt', function(err, result) {
        if (err) {
            reject(err);
        } else {
            resolve(result);
        }
    });
});
```

The executor function usually initiates some asynchronous operation. Once it is finished, the executor should call `resolve` with the result, or `reject` if an error occurred.

The return value of the executor is ignored. Returning a value from an executor function is a possible error because the returned value cannot be used and it doesn't affect the promise in any way.

## 规则详解

This rule disallows returning values from Promise executor functions.

Only `return` without a value is allowed, as it's a control flow statement.

此规则的 **错误** 代码实例：



```js
/*eslint no-promise-executor-return: "error"*/

new Promise((resolve, reject) => {
    if (someCondition) {
        return defaultResult;
    }
    getSomething((err, result) => {
        if (err) {
            reject(err);
        } else {
            resolve(result);
        }
    });
});

new Promise((resolve, reject) => getSomething((err, data) => {
    if (err) {
        reject(err);
    } else {
        resolve(data);
    }
}));

new Promise(() => {
    return 1;
});
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-promise-executor-return: "error"*/

new Promise((resolve, reject) => {
    if (someCondition) {
        resolve(defaultResult);
        return;
    }
    getSomething((err, result) => {
        if (err) {
            reject(err);
        } else {
            resolve(result);
        }
    });
});

new Promise((resolve, reject) => {
    getSomething((err, data) => {
        if (err) {
            reject(err);
        } else {
            resolve(data);
        }
    });
});

Promise.resolve(1);
```
