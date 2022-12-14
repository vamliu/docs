---
规则名: no-dupe-else-if
规则类型: problem
关联规则:
- no-duplicate-case
- no-lonely-if
---



`if-else-if` chains are commonly used when there is a need to execute only one branch (or at most one branch) out of several possible branches, based on certain conditions.

```js
if (a) {
    foo();
} else if (b) {
    bar();
} else if (c) {
    baz();
}
```

Two identical test conditions in the same chain are almost always a mistake in the code. Unless there are side effects in the expressions, a duplicate will evaluate to the same `true` or `false` value as the identical expression earlier in the chain, meaning that its branch can never execute.

```js
if (a) {
    foo();
} else if (b) {
    bar();
} else if (b) {
    baz();
}
```

In the above example, `baz()` can never execute. Obviously, `baz()` could be executed only when `b` evaluates to `true`, but in that case `bar()` would be executed instead, since it's earlier in the chain.

## 规则详解

This rule disallows duplicate conditions in the same `if-else-if` chain.

此规则的 **错误** 代码实例：



```js
/*eslint no-dupe-else-if: "error"*/

if (isSomething(x)) {
    foo();
} else if (isSomething(x)) {
    bar();
}

if (a) {
    foo();
} else if (b) {
    bar();
} else if (c && d) {
    baz();
} else if (c && d) {
    quux();
} else {
    quuux();
}

if (n === 1) {
    foo();
} else if (n === 2) {
    bar();
} else if (n === 3) {
    baz();
} else if (n === 2) {
    quux();
} else if (n === 5) {
    quuux();
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-dupe-else-if: "error"*/

if (isSomething(x)) {
    foo();
} else if (isSomethingElse(x)) {
    bar();
}

if (a) {
    foo();
} else if (b) {
    bar();
} else if (c && d) {
    baz();
} else if (c && e) {
    quux();
} else {
    quuux();
}

if (n === 1) {
    foo();
} else if (n === 2) {
    bar();
} else if (n === 3) {
    baz();
} else if (n === 4) {
    quux();
} else if (n === 5) {
    quuux();
}
```

This rule can also detect some cases where the conditions are not identical, but the branch can never execute due to the logic of `||` and `&&` operators.

Examples of additional **incorrect** code for this rule:



```js
/*eslint no-dupe-else-if: "error"*/

if (a || b) {
    foo();
} else if (a) {
    bar();
}

if (a) {
    foo();
} else if (b) {
    bar();
} else if (a || b) {
    baz();
}

if (a) {
    foo();
} else if (a && b) {
    bar();
}

if (a && b) {
    foo();
} else if (a && b && c) {
    bar();
}

if (a || b) {
    foo();
} else if (b && c) {
    bar();
}

if (a) {
    foo();
} else if (b && c) {
    bar();
} else if (d && (c && e && b || a)) {
    baz();
}
```

Please note that this rule does not compare conditions from the chain with conditions inside statements, and will not warn in the cases such as follows:

```js
if (a) {
    if (a) {
        foo();
    }
}

if (a) {
    foo();
} else {
    if (a) {
        bar();
    }
}
```

## 禁用建议

In rare cases where you really need identical test conditions in the same chain, which necessarily means that the expressions in the chain are causing and relying on side effects, you will have to turn this rule off.
