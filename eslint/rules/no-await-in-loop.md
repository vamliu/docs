---
规则名: no-await-in-loop
规则类型: problem
---


Performing an operation on each element of an iterable is a common task. However, performing an
`await` as part of each operation is an indication that the program is not taking full advantage of
the parallelization benefits of `async`/`await`.

Usually, the code should be refactored to create all the promises at once, then get access to the
results using `Promise.all()`. Otherwise, each successive operation will not start until the
previous one has completed.

Concretely, the following function should be refactored as shown:

```js
async function foo(things) {
  const results = [];
  for (const thing of things) {
    // 错误: each loop iteration is delayed until the entire asynchronous operation completes
    results.push(await bar(thing));
  }
  return baz(results);
}
```

```js
async function foo(things) {
  const results = [];
  for (const thing of things) {
    // 正确: all asynchronous operations are immediately started.
    results.push(bar(thing));
  }
  // Now that all the asynchronous operations are running, here we wait until they all complete.
  return baz(await Promise.all(results));
}
```

## 规则详解

This rule disallows the use of `await` within loop bodies.

## Examples

此规则的 **正确** 代码实例：

```js
/*eslint no-await-in-loop: "error"*/

async function foo(things) {
  const results = [];
  for (const thing of things) {
    // 正确: all asynchronous operations are immediately started.
    results.push(bar(thing));
  }
  // Now that all the asynchronous operations are running, here we wait until they all complete.
  return baz(await Promise.all(results));
}
```

此规则的 **错误** 代码实例：

```js
/*eslint no-await-in-loop: "error"*/

async function foo(things) {
  const results = [];
  for (const thing of things) {
    // 错误: each loop iteration is delayed until the entire asynchronous operation completes
    results.push(await bar(thing));
  }
  return baz(results);
}
```

## 禁用建议

In many cases the iterations of a loop are not actually independent of each-other. For example, the
output of one iteration might be used as the input to another. Or, loops may be used to retry
asynchronous operations that were unsuccessful. Or, loops may be used to prevent your code from sending
an excessive amount of requests in parallel. In such cases it makes sense to use `await` within a
loop and it is recommended to disable the rule via a standard ESLint disable comment.
