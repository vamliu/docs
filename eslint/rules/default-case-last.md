---
规则名: default-case-last
规则类型: suggestion
关联规则:
- default-case
深入了解:
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/switch
---


A `switch` statement can optionally have a `default` clause.

If present, it's usually the last clause, but it doesn't need to be. It is also allowed to put the `default` clause before all `case` clauses, or anywhere between. The behavior is mostly the same as if it was the last clause. The `default` block will be still executed only if there is no match in the `case` clauses (including those defined after the `default`), but there is also the ability to "fall through" from the `default` clause to the following clause in the list. However, such flow is not common and it would be confusing to the readers.

Even if there is no "fall through" logic, it's still unexpected to see the `default` clause before or between the `case` clauses. By convention, it is expected to be the last clause.

If a `switch` statement should have a `default` clause, it's considered a best practice to define it as the last clause.

## 规则详解

This rule enforces `default` clauses in `switch` statements to be last.

It applies only to `switch` statements that already have a `default` clause.

This rule does not enforce the existence of `default` clauses. See [default-case](default-case) if you also want to enforce the existence of `default` clauses in `switch` statements.

此规则的 **错误** 代码实例：

```js
/*eslint default-case-last: "error"*/

switch (foo) {
    default:
        bar();
        break;
    case "a":
        baz();
        break;
}

switch (foo) {
    case 1:
        bar();
        break;
    default:
        baz();
        break;
    case 2:
        quux();
        break;
}

switch (foo) {
    case "x":
        bar();
        break;
    default:
    case "y":
        baz();
        break;
}

switch (foo) {
    default:
        break;
    case -1:
        bar();
        break;
}

switch (foo) {
  default:
    doSomethingIfNotZero();
  case 0:
    doSomethingAnyway();
}
```

此规则的 **正确** 代码实例：

```js
/*eslint default-case-last: "error"*/

switch (foo) {
    case "a":
        baz();
        break;
    default:
        bar();
        break;
}

switch (foo) {
    case 1:
        bar();
        break;
    case 2:
        quux();
        break;
    default:
        baz();
        break;
}

switch (foo) {
    case "x":
        bar();
        break;
    case "y":
    default:
        baz();
        break;
}

switch (foo) {
    case -1:
        bar();
        break;
}

if (foo !== 0) {
    doSomethingIfNotZero();
}
doSomethingAnyway();
```
