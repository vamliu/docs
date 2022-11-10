---
规则名: no-sequences
规则类型: suggestion
---


The comma operator includes multiple expressions where only one is expected. It evaluates each operand from left to right and returns the value of the last operand. However, this frequently obscures side effects, and its use is often an accident. Here are some examples of sequences:

```js
var a = (3, 5); // a = 5

a = b += 5, a + b;

while (a = next(), a && a.length);

(0, eval)("doSomething();");
```

## 规则详解

This rule forbids the use of the comma operator, with the following exceptions:

* In the initialization or update portions of a `for` statement.
* By default, if the expression sequence is explicitly wrapped in parentheses. This exception can be removed with the `allowInParentheses` option.

此规则的 **错误** 代码实例：



```js
/*eslint no-sequences: "error"*/

foo = doSomething(), val;

0, eval("doSomething();");

do {} while (doSomething(), !!test);

for (; doSomething(), !!test; );

if (doSomething(), !!test);

switch (val = foo(), val) {}

while (val = foo(), val < 42);

with (doSomething(), val) {}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-sequences: "error"*/

foo = (doSomething(), val);

(0, eval)("doSomething();");

do {} while ((doSomething(), !!test));

for (i = 0, j = 10; i < j; i++, j--);

if ((doSomething(), !!test));

switch ((val = foo(), val)) {}

while ((val = foo(), val < 42));

with ((doSomething(), val)) {}
```

### Note about arrow function bodies

If an arrow function body is a statement rather than a block, and that statement contains a sequence, you need to use double parentheses around the statement to indicate that the sequence is intentional.

Examples of **incorrect** code for arrow functions:



```js
/*eslint no-sequences: "error"*/
const foo = (val) => (console.log('bar'), val);

const foo = () => ((bar = 123), 10);

const foo = () => { return (bar = 123), 10 }
```

Examples of **correct** code for arrow functions:

::: correct

```js
/*eslint no-sequences: "error"*/
const foo = (val) => ((console.log('bar'), val));

const foo = () => (((bar = 123), 10));

const foo = () => { return ((bar = 123), 10) }
```

## 配置项

This rule takes one option, an object, with the following properties:

* `"allowInParentheses"`: If set to `true` (default), this rule allows expression sequences that are explicitly wrapped in parentheses.

### allowInParentheses

选项 `{ "allowInParentheses": false }` 的 **错误** 代码示例：



```js
/*eslint no-sequences: ["error", { "allowInParentheses": false }]*/

foo = (doSomething(), val);

(0, eval)("doSomething();");

do {} while ((doSomething(), !!test));

for (; (doSomething(), !!test); );

if ((doSomething(), !!test));

switch ((val = foo(), val)) {}

while ((val = foo(), val < 42));

with ((doSomething(), val)) {}

const foo = (val) => ((console.log('bar'), val));
```

选项 `{ "allowInParentheses": false }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-sequences: ["error", { "allowInParentheses": false }]*/

for (i = 0, j = 10; i < j; i++, j--);
```

## 禁用建议

Disable this rule if sequence expressions with the comma operator are acceptable.
Another case is where you might want to report all usages of the comma operator, even in a for loop. You can achieve this using rule `no-restricted-syntax`:

```js
{
    "rules": {
        "no-restricted-syntax": ["error", "SequenceExpression"]
    }
}
```
