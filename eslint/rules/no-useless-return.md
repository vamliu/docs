---
规则名: no-useless-return
规则类型: suggestion
---



A `return;` statement with nothing after it is redundant, and has no effect on the runtime behavior of a function. This can be confusing, so it's better to disallow these redundant statements.

## 规则详解

This rule aims to report redundant `return` statements.

此规则的 **错误** 代码实例：



```js
/* eslint no-useless-return: "error" */

function foo() { return; }

function foo() {
  doSomething();
  return;
}

function foo() {
  if (condition) {
    bar();
    return;
  } else {
    baz();
  }
}

function foo() {
  switch (bar) {
    case 1:
      doSomething();
    default:
      doSomethingElse();
      return;
  }
}

```

此规则的 **正确** 代码实例：

::: correct

```js
/* eslint no-useless-return: "error" */

function foo() { return 5; }

function foo() {
  return doSomething();
}

function foo() {
  if (condition) {
    bar();
    return;
  } else {
    baz();
  }
  qux();
}

function foo() {
  switch (bar) {
    case 1:
      doSomething();
      return;
    default:
      doSomethingElse();
  }
}

function foo() {
  for (const foo of bar) {
    return;
  }
}

```

## 禁用建议

If you don't care about disallowing redundant return statements, you can turn off this rule.
