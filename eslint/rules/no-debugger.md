---
规则名: no-debugger
规则类型: problem
关联规则:
- no-alert
- no-console
深入了解:
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/debugger
---



The `debugger` statement is used to tell the executing JavaScript environment to stop execution and start up a debugger at the current point in the code. This has fallen out of favor as a good practice with the advent of modern debugging and development tools. Production code should definitely not contain `debugger`, as it will cause the browser to stop executing code and open an appropriate debugger.

## 规则详解

This rule disallows `debugger` statements.

Example of **incorrect** code for this rule:



```js
/*eslint no-debugger: "error"*/

function isTruthy(x) {
    debugger;
    return Boolean(x);
}
```

Example of **correct** code for this rule:

::: correct

```js
/*eslint no-debugger: "error"*/

function isTruthy(x) {
    return Boolean(x); // set a breakpoint at this line
}
```

## 禁用建议

If your code is still very much in development and don't want to worry about stripping `debugger` statements, then turn this rule off. You'll generally want to turn it back on when testing code prior to deployment.
