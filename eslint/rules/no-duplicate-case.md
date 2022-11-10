---
规则名: no-duplicate-case
规则类型: problem
---



If a `switch` statement has duplicate test expressions in `case` clauses, it is likely that a programmer copied a `case` clause but forgot to change the test expression.

## 规则详解

This rule disallows duplicate test expressions in `case` clauses of `switch` statements.

此规则的 **错误** 代码实例：

```js
/*eslint no-duplicate-case: "error"*/

var a = 1,
    one = 1;

switch (a) {
    case 1:
        break;
    case 2:
        break;
    case 1:         // duplicate test expression
        break;
    default:
        break;
}

switch (a) {
    case one:
        break;
    case 2:
        break;
    case one:         // duplicate test expression
        break;
    default:
        break;
}

switch (a) {
    case "1":
        break;
    case "2":
        break;
    case "1":         // duplicate test expression
        break;
    default:
        break;
}
```

此规则的 **正确** 代码实例：

```js
/*eslint no-duplicate-case: "error"*/

var a = 1,
    one = 1;

switch (a) {
    case 1:
        break;
    case 2:
        break;
    case 3:
        break;
    default:
        break;
}

switch (a) {
    case one:
        break;
    case 2:
        break;
    case 3:
        break;
    default:
        break;
}

switch (a) {
    case "1":
        break;
    case "2":
        break;
    case "3":
        break;
    default:
        break;
}
```

## 禁用建议

In rare cases where identical test expressions in `case` clauses produce different values, which necessarily means that the expressions are causing and relying on side effects, you will have to disable this rule.

```js
switch (a) {
    case i++:
        foo();
        break;
    case i++: // eslint-disable-line no-duplicate-case
        bar();
        break;
}
```
