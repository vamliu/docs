---
规则名: prefer-const
布局: doc
规则类型: suggestion
关联规则:
- no-var
- no-use-before-define
---



If a variable is never reassigned, using the `const` declaration is better.

`const` declaration tells readers, "this variable is never reassigned," reducing cognitive load and improving maintainability.

## 规则详解

This rule is aimed at flagging variables that are declared using `let` keyword, but never reassigned after the initial assignment.

Examples of **incorrect** code for this rule:



```js
/*eslint prefer-const: "error"*/

// it's initialized and never reassigned.
let a = 3;
console.log(a);

let a;
a = 0;
console.log(a);

class C {
    static {
        let a;
        a = 0;
        console.log(a);
    }
}

// `i` is redefined (not reassigned) on each loop step.
for (let i in [1, 2, 3]) {
    console.log(i);
}

// `a` is redefined (not reassigned) on each loop step.
for (let a of [1, 2, 3]) {
    console.log(a);
}
```

Examples of **correct** code for this rule:

::: correct

```js
/*eslint prefer-const: "error"*/

// using const.
const a = 0;

// it's never initialized.
let a;
console.log(a);

// it's reassigned after initialized.
let a;
a = 0;
a = 1;
console.log(a);

// it's initialized in a different block from the declaration.
let a;
if (true) {
    a = 0;
}
console.log(a);

// it's initialized in a different scope.
let a;
class C {
    #x;
    static {
        a = obj => obj.#x;
    }
}

// it's initialized at a place that we cannot write a variable declaration.
let a;
if (true) a = 0;
console.log(a);

// `i` gets a new binding each iteration
for (const i in [1, 2, 3]) {
  console.log(i);
}

// `a` gets a new binding each iteration
for (const a of [1, 2, 3]) {
  console.log(a);
}

// `end` is never reassigned, but we cannot separate the declarations without modifying the scope.
for (let i = 0, end = 10; i < end; ++i) {
    console.log(a);
}

// `predicate` is only assigned once but cannot be separately declared as `const`
let predicate;
[object.type, predicate] = foo();

// `a` is only assigned once but cannot be separately declared as `const`
let a;
const b = {};
({ a, c: b.c } = func());

// suggest to use `no-var` rule.
var b = 3;
console.log(b);
```

## 配置项

```json
{
    "prefer-const": ["error", {
        "destructuring": "any",
        "ignoreReadBeforeAssign": false
    }]
}
```

### destructuring

The kind of the way to address variables in destructuring.
There are 2 values:

* `"any"` (default) - If any variables in destructuring should be `const`, this rule warns for those variables.
* `"all"` - If all variables in destructuring should be `const`, this rule warns the variables. Otherwise, ignores them.

选项 default `{"destructuring": "any"}` 的 **错误** 代码示例：



```js
/*eslint prefer-const: "error"*/
/*eslint-env es6*/

let {a, b} = obj;    /*error 'b' is never reassigned, use 'const' instead.*/
a = a + 1;
```

选项 default `{"destructuring": "any"}` 的 **正确** 代码示例：

::: correct

```js
/*eslint prefer-const: "error"*/
/*eslint-env es6*/

// using const.
const {a: a0, b} = obj;
const a = a0 + 1;

// all variables are reassigned.
let {a, b} = obj;
a = a + 1;
b = b + 1;
```

选项 `{"destructuring": "all"}` 的 **错误** 代码示例：



```js
/*eslint prefer-const: ["error", {"destructuring": "all"}]*/
/*eslint-env es6*/

// all of `a` and `b` should be const, so those are warned.
let {a, b} = obj;    /*error 'a' is never reassigned, use 'const' instead.
                             'b' is never reassigned, use 'const' instead.*/
```

选项 `{"destructuring": "all"}` 的 **正确** 代码示例：

::: correct

```js
/*eslint prefer-const: ["error", {"destructuring": "all"}]*/
/*eslint-env es6*/

// 'b' is never reassigned, but all of `a` and `b` should not be const, so those are ignored.
let {a, b} = obj;
a = a + 1;
```

### ignoreReadBeforeAssign

This is an option to avoid conflicting with `no-use-before-define` rule (without `"nofunc"` option).
If `true` is specified, this rule will ignore variables that are read between the declaration and the first assignment.
Default is `false`.

选项 `{"ignoreReadBeforeAssign": true}` 的 **正确** 代码示例：

::: correct

```js
/*eslint prefer-const: ["error", {"ignoreReadBeforeAssign": true}]*/
/*eslint-env es6*/

let timer;
function initialize() {
    if (foo()) {
        clearInterval(timer);
    }
}
timer = setInterval(initialize, 100);
```

选项 default `{"ignoreReadBeforeAssign": false}` 的 **正确** 代码示例：

::: correct

```js
/*eslint prefer-const: ["error", {"ignoreReadBeforeAssign": false}]*/
/*eslint-env es6*/

const timer = setInterval(initialize, 100);
function initialize() {
    if (foo()) {
        clearInterval(timer);
    }
}
```

## 使用建议

If you don't want to be notified about variables that are never reassigned after initial assignment, you can safely disable this rule.
