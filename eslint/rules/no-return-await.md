---
规则名: no-return-await
规则类型: suggestion
深入了解:
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function
- https://jakearchibald.com/2017/await-vs-return-vs-return-await/
---


Using `return await` inside an `async function` keeps the current function in the call stack until the Promise that is being awaited has resolved, at the cost of an extra microtask before resolving the outer Promise. `return await` can also be used in a try/catch statement to catch errors from another function that returns a Promise.

You can avoid the extra microtask by not awaiting the return value, with the trade off of the function no longer being a part of the stack trace if an error is thrown asynchronously from the Promise being returned. This can make debugging more difficult.

## 规则详解

This rule aims to prevent a likely common performance hazard due to a lack of understanding of the semantics of `async function`.

此规则的 **错误** 代码实例：



```js
/*eslint no-return-await: "error"*/

async function foo() {
    return await bar();
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-return-await: "error"*/

async function foo() {
    return bar();
}

async function foo() {
    await bar();
    return;
}

// This is essentially the same as `return await bar();`, but the rule checks only `await` in `return` statements
async function foo() {
    const x = await bar();
    return x;
}

// In this example the `await` is necessary to be able to catch errors thrown from `bar()`
async function foo() {
    try {
        return await bar();
    } catch (error) {}
}
```

## 禁用建议

There are a few reasons you might want to turn this rule off:

* If you want to use `await` to denote a value that is a thenable
* If you do not want the performance benefit of avoiding `return await`
* If you want the functions to show up in stack traces (useful for debugging purposes)
