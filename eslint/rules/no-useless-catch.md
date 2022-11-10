---
规则名: no-useless-catch
规则类型: suggestion
---



A `catch` clause that only rethrows the original error is redundant, and has no effect on the runtime behavior of the program. These redundant clauses can be a source of confusion and code bloat, so it's better to disallow these unnecessary `catch` clauses.

## 规则详解

This rule reports `catch` clauses that only `throw` the caught error.

此规则的 **错误** 代码实例：



```js
/*eslint no-useless-catch: "error"*/

try {
  doSomethingThatMightThrow();
} catch (e) {
  throw e;
}

try {
  doSomethingThatMightThrow();
} catch (e) {
  throw e;
} finally {
  cleanUp();
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-useless-catch: "error"*/

try {
  doSomethingThatMightThrow();
} catch (e) {
  doSomethingBeforeRethrow();
  throw e;
}

try {
  doSomethingThatMightThrow();
} catch (e) {
  handleError(e);
}

try {
  doSomethingThatMightThrow();
} finally {
  cleanUp();
}
```

## 禁用建议

If you don't want to be notified about unnecessary catch clauses, you can safely disable this rule.
