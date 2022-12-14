---
规则名: no-extra-parens
规则类型: layout
关联规则:
- arrow-parens
- no-cond-assign
- no-return-assign
深入了解:
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence
---



This rule restricts the use of parentheses to only where they are necessary.

## 规则详解

This rule always ignores extra parentheses around the following:

* RegExp literals such as `(/abc/).test(var)` to avoid conflicts with the [wrap-regex](wrap-regex) rule
* immediately-invoked function expressions (also known as IIFEs) such as `var x = (function () {})();` and `var x = (function () {}());` to avoid conflicts with the [wrap-iife](wrap-iife) rule
* arrow function arguments to avoid conflicts with the [arrow-parens](arrow-parens) rule

## 配置项

This rule has a string option:

* `"all"` (default) disallows unnecessary parentheses around *any* expression
* `"functions"` disallows unnecessary parentheses *only* around function expressions

This rule has an object option for exceptions to the `"all"` option:

* `"conditionalAssign": false` allows extra parentheses around assignments in conditional test expressions
* `"returnAssign": false` allows extra parentheses around assignments in `return` statements
* `"nestedBinaryExpressions": false` allows extra parentheses in nested binary expressions
* `"ignoreJSX": "none|all|multi-line|single-line"` allows extra parentheses around no/all/multi-line/single-line JSX components. Defaults to `none`.
* `"enforceForArrowConditionals": false` allows extra parentheses around ternary expressions which are the body of an arrow function
* `"enforceForSequenceExpressions": false` allows extra parentheses around sequence expressions
* `"enforceForNewInMemberExpressions": false` allows extra parentheses around `new` expressions in member expressions
* `"enforceForFunctionPrototypeMethods": false` allows extra parentheses around immediate `.call` and `.apply` method calls on function expressions and around function expressions in the same context.

### all

选项 `"all"`  默认值的 **错误** 代码示例：



```js
/* eslint no-extra-parens: "error" */

a = (b * c);

(a * b) + c;

for (a in (b, c));

for (a in (b));

for (a of (b));

typeof (a);

(function(){} ? a() : b());

class A {
    [(x)] = 1;
}

class B {
    x = (y + z);
}
```

选项 `"all"` 默认值的 **正确** 代码示例：

::: correct

```js
/* eslint no-extra-parens: "error" */

(0).toString();

(Object.prototype.toString.call());

({}.toString.call());

(function(){}) ? a() : b();

(/^a$/).test(x);

for (a of (b, c));

for (a of b);

for (a in b, c);

for (a in b);

class A {
    [x] = 1;
}

class B {
    x = y + z;
}
```

### conditionalAssign

选项 `"all"` and `{ "conditionalAssign": false }`  的 **正确** 代码示例：

::: correct

```js
/* eslint no-extra-parens: ["error", "all", { "conditionalAssign": false }] */

while ((foo = bar())) {}

if ((foo = bar())) {}

do; while ((foo = bar()))

for (;(a = b););
```

### returnAssign

选项 `"all"` and `{ "returnAssign": false }`  的 **正确** 代码示例：

::: correct

```js
/* eslint no-extra-parens: ["error", "all", { "returnAssign": false }] */

function a(b) {
  return (b = 1);
}

function a(b) {
  return b ? (c = d) : (c = e);
}

b => (b = 1);

b => b ? (c = d) : (c = e);
```

### nestedBinaryExpressions

选项 `"all"` and `{ "nestedBinaryExpressions": false }`  的 **正确** 代码示例：

::: correct

```js
/* eslint no-extra-parens: ["error", "all", { "nestedBinaryExpressions": false }] */

x = a || (b && c);
x = a + (b * c);
x = (a * b) / c;
```

### ignoreJSX

选项 `all` and `{ "ignoreJSX": "all" }`  的 **正确** 代码示例：

::: correct

```js
/* eslint no-extra-parens: ["error", "all", { ignoreJSX: "all" }] */
const Component = (<div />)
const Component = (
    <div
        prop={true}
    />
)
```

选项 `all` and `{ "ignoreJSX": "multi-line" }`  的 **错误** 代码示例：



```js
/* eslint no-extra-parens: ["error", "all", { ignoreJSX: "multi-line" }] */
const Component = (<div />)
const Component = (<div><p /></div>)
```

选项 `all` and `{ "ignoreJSX": "multi-line" }`  的 **正确** 代码示例：

::: correct

```js
/* eslint no-extra-parens: ["error", "all", { ignoreJSX: "multi-line" }] */
const Component = (
    <div>
        <p />
    </div>
)
const Component = (
    <div
        prop={true}
    />
)
```

选项 `all` and `{ "ignoreJSX": "single-line" }`  的 **错误** 代码示例：



```js
/* eslint no-extra-parens: ["error", "all", { ignoreJSX: "single-line" }] */
const Component = (
    <div>
        <p />
    </div>
)
const Component = (
    <div
        prop={true}
    />
)
```

选项 `all` and `{ "ignoreJSX": "single-line" }`  的 **正确** 代码示例：

::: correct

```js
/* eslint no-extra-parens: ["error", "all", { ignoreJSX: "single-line" }] */
const Component = (<div />)
const Component = (<div><p /></div>)
```

### enforceForArrowConditionals

选项 `"all"` and `{ "enforceForArrowConditionals": false }`  的 **正确** 代码示例：

::: correct

```js
/* eslint no-extra-parens: ["error", "all", { "enforceForArrowConditionals": false }] */

const b = a => 1 ? 2 : 3;
const d = c => (1 ? 2 : 3);
```

### enforceForSequenceExpressions

选项 `"all"` and `{ "enforceForSequenceExpressions": false }`  的 **正确** 代码示例：

::: correct

```js
/* eslint no-extra-parens: ["error", "all", { "enforceForSequenceExpressions": false }] */

(a, b);

if ((val = foo(), val < 10)) {}

while ((val = foo(), val < 10));
```

### enforceForNewInMemberExpressions

选项 `"all"` and `{ "enforceForNewInMemberExpressions": false }`  的 **正确** 代码示例：

::: correct

```js
/* eslint no-extra-parens: ["error", "all", { "enforceForNewInMemberExpressions": false }] */

const foo = (new Bar()).baz;

const quux = (new Bar())[baz];

(new Bar()).doSomething();
```

### enforceForFunctionPrototypeMethods

选项 `"all"` and `{ "enforceForFunctionPrototypeMethods": false }`  的 **正确** 代码示例：

::: correct

```js
/* eslint no-extra-parens: ["error", "all", { "enforceForFunctionPrototypeMethods": false }] */

const foo = (function () {}).call();

const bar = (function () {}).apply();

const baz = (function () {}.call());

const quux = (function () {}.apply());
```

### functions

选项 `"functions"` 的 **错误** 代码示例：



```js
/* eslint no-extra-parens: ["error", "functions"] */

((function foo() {}))();

var y = (function () {return 1;});
```

选项 `"functions"` 的 **正确** 代码示例：

::: correct

```js
/* eslint no-extra-parens: ["error", "functions"] */

(0).toString();

(Object.prototype.toString.call());

({}.toString.call());

(function(){} ? a() : b());

(/^a$/).test(x);

a = (b * c);

(a * b) + c;

typeof (a);
```
