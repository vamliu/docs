---
规则名: no-process-exit
规则类型: suggestion
---


This rule was **deprecated** in ESLint v7.0.0. Please use the corresponding rule in [`eslint-plugin-node`](https://github.com/mysticatea/eslint-plugin-node).

The `process.exit()` method in Node.js is used to immediately stop the Node.js process and exit. This is a dangerous operation because it can occur in any method at any point in time, potentially stopping a Node.js application completely when an error occurs. For example:

```js
if (somethingBadHappened) {
    console.error("Something bad happened!");
    process.exit(1);
}
```

This code could appear in any module and will stop the entire application when `somethingBadHappened` is truthy. This doesn't give the application any chance to respond to the error. It's usually better to throw an error and allow the application to handle it appropriately:

```js
if (somethingBadHappened) {
    throw new Error("Something bad happened!");
}
```

By throwing an error in this way, other parts of the application have an opportunity to handle the error rather than stopping the application altogether. If the error bubbles all the way up to the process without being handled, then the process will exit and a non-zero exit code will returned, so the end result is the same.

If you are using `process.exit()` only for specifying the exit code, you can set [`process.exitCode`](https://nodejs.org/api/process.html#process_process_exitcode) (introduced in Node.js 0.11.8) instead.

## 规则详解

This rule aims to prevent the use of `process.exit()` in Node.js JavaScript. As such, it warns whenever `process.exit()` is found in code.

此规则的 **错误** 代码实例：



```js
/*eslint no-process-exit: "error"*/

process.exit(1);
process.exit(0);
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-process-exit: "error"*/

Process.exit();
var exit = process.exit;
```

## 禁用建议

There may be a part of a Node.js application that is responsible for determining the correct exit code to return upon exiting. In that case, you should turn this rule off to allow proper handling of the exit code.
