---
规则名: no-ex-assign
布局: doc
规则类型: problem
深入了解:
- https://bocoup.com/blog/the-catch-with-try-catch
---



If a `catch` clause in a `try` statement accidentally (or purposely) assigns another value to the exception parameter, it is impossible to refer to the error from that point on.
Since there is no `arguments` object to offer alternative access to this data, assignment of the parameter is absolutely destructive.

## 规则详解

This rule disallows reassigning exceptions in `catch` clauses.

Examples of **incorrect** code for this rule:



```js
/*eslint no-ex-assign: "error"*/

try {
    // code
} catch (e) {
    e = 10;
}
```

Examples of **correct** code for this rule:

::: correct

```js
/*eslint no-ex-assign: "error"*/

try {
    // code
} catch (e) {
    var foo = 10;
}
```
