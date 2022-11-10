---
规则名: space-infix-ops
规则类型: layout
---



While formatting preferences are very personal, a number of style guides require spaces around operators, such as:

```js
var sum = 1 + 2;
```

Proponents of this rule believe that it makes code easier to read and can more easily highlight potential errors, such as:

```js
var sum = i+++2;
```

While this is valid JavaScript syntax, it is hard to determine what the author intended.

## 规则详解

This rule is aimed at ensuring there are spaces around infix operators.

## 配置项

This rule accepts a single options argument with the following defaults:

```json
"space-infix-ops": ["error", { "int32Hint": false }]
```

### `int32Hint`

Set the `int32Hint` option to `true` (default is `false`) to allow write `a|0` without space.

```js
var foo = bar|0; // `foo` is forced to be signed 32 bit integer
```

此规则的 **错误** 代码实例：



```js
/*eslint space-infix-ops: "error"*/
/*eslint-env es6*/

a+b

a+ b

a +b

a?b:c

const a={b:1};

var {a=0}=bar;

function foo(a=0) { }
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint space-infix-ops: "error"*/
/*eslint-env es6*/

a + b

a       + b

a ? b : c

const a = {b:1};

var {a = 0} = bar;

function foo(a = 0) { }
```

## 禁用建议

You can turn this rule off if you are not concerned with the consistency of spacing around infix operators.
