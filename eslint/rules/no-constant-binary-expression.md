---
规则名: no-constant-binary-expression
规则类型: problem
关联规则:
- no-constant-condition
深入了解:
- https://eslint.org/blog/2022/07/interesting-bugs-caught-by-no-constant-binary-expression/
---


Comparisons which will always evaluate to true or false and logical expressions (`||`, `&&`, `??`) which either always short-circuit or never short-circuit are both likely indications of programmer error.

These errors are especially common in complex expressions where operator precedence is easy to misjudge. For example:

```js
// One might think this would evaluate as `a + (b ?? c)`:
const x = a + b ?? c;

// But it actually evaluates as `(a + b) ?? c`. Since `a + b` can never be null,
// the `?? c` has no effect.
```

Additionally, this rule detects comparisons to newly constructed objects/arrays/functions/etc. In JavaScript, where objects are compared by reference, a newly constructed object can _never_ `===` any other value. This can be surprising for programmers coming from languages where objects are compared by value.

```js
// Programmers coming from a language where objects are compared by value might expect this to work:
const isEmpty = x === [];

// However, this will always result in `isEmpty` being `false`.
```

## 规则详解

This rule identifies `==` and `===` comparisons which, based on the semantics of the JavaScript language, will always evaluate to `true` or `false`.

It also identifies `||`, `&&` and `??` logical expressions which will either always or never short-circuit.

此规则的 **错误** 代码实例：



```js
/*eslint no-constant-binary-expression: "error"*/

const value1 = +x == null;

const value2 = condition ? x : {} || DEFAULT;

const value3 = !foo == null;

const value4 = new Boolean(foo) === true;

const objIsEmpty = someObj === {};

const arrIsEmpty = someArr === [];
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-constant-binary-expression: "error"*/

const value1 = x == null;

const value2 = (condition ? x : {}) || DEFAULT;

const value3 = !(foo == null);

const value4 = Boolean(foo) === true;

const objIsEmpty = Object.keys(someObj).length === 0;

const arrIsEmpty = someArr.length === 0;
```
