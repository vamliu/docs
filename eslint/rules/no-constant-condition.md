---
规则名: no-constant-condition
规则类型: problem
关联规则:
- no-constant-binary-expression
---



A constant expression (for example, a literal) as a test condition might be a typo or development trigger for a specific behavior. For example, the following code looks as if it is not ready for production.

```js
if (false) {
    doSomethingUnfinished();
}
```

## 规则详解

This rule disallows constant expressions in the test condition of:

* `if`, `for`, `while`, or `do...while` statement
* `?:` ternary expression

此规则的 **错误** 代码实例：



```js
/*eslint no-constant-condition: "error"*/

if (false) {
    doSomethingUnfinished();
}

if (void x) {
    doSomethingUnfinished();
}

if (x &&= false) {
    doSomethingNever();
}

if (class {}) {
    doSomethingAlways();
}

if (new Boolean(x)) {
    doSomethingAlways();
}

if (Boolean(1)) {
    doSomethingAlways();
}

if (undefined) {
    doSomethingUnfinished();
}

if (x ||= true) {
    doSomethingAlways();
}

for (;-2;) {
    doSomethingForever();
}

while (typeof x) {
    doSomethingForever();
}

do {
    doSomethingForever();
} while (x = -1);

var result = 0 ? a : b;
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-constant-condition: "error"*/

if (x === 0) {
    doSomething();
}

for (;;) {
    doSomethingForever();
}

while (typeof x === "undefined") {
    doSomething();
}

do {
    doSomething();
} while (x);

var result = x !== 0 ? a : b;
```

## 配置项

### checkLoops

Set to `true` by default. Setting this option to `false` allows constant expressions in loops.

Examples of **correct** code for when `checkLoops` is `false`:

::: correct

```js
/*eslint no-constant-condition: ["error", { "checkLoops": false }]*/

while (true) {
    doSomething();
    if (condition()) {
        break;
    }
};

for (;true;) {
    doSomething();
    if (condition()) {
        break;
    }
};

do {
    doSomething();
    if (condition()) {
        break;
    }
} while (true)
```
