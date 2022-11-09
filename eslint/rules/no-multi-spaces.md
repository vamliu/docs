---
规则名: no-multi-spaces
布局: doc
规则类型: layout
关联规则:
- key-spacing
- space-infix-ops
- space-in-brackets
- space-in-parens
- space-after-keywords
- space-unary-ops
- space-return-throw-case
---



Multiple spaces in a row that are not used for indentation are typically mistakes. For example:

```js

if(foo  === "bar") {}

```

It's hard to tell, but there are two spaces between `foo` and `===`. Multiple spaces such as this are generally frowned upon in favor of single spaces:

```js

if(foo === "bar") {}

```

## 规则详解

This rule aims to disallow multiple whitespace around logical expressions, conditional expressions, declarations, array elements, object properties, sequences and function parameters.

Examples of **incorrect** code for this rule:



```js
/*eslint no-multi-spaces: "error"*/

var a =  1;

if(foo   === "bar") {}

a <<  b

var arr = [1,  2];

a ?  b: c
```

Examples of **correct** code for this rule:

::: correct

```js
/*eslint no-multi-spaces: "error"*/

var a = 1;

if(foo === "bar") {}

a << b

var arr = [1, 2];

a ? b: c
```

## 配置项

This rule's configuration consists of an object with the following properties:

* `"ignoreEOLComments": true` (defaults to `false`) ignores multiple spaces before comments that occur at the end of lines
* `"exceptions": { "Property": true }` (`"Property"` is the only node specified by default) specifies nodes to ignore

### ignoreEOLComments

Examples of **incorrect** code for this rule with the `{ "ignoreEOLComments": false }` (default) option:



```js
/*eslint no-multi-spaces: ["error", { ignoreEOLComments: false }]*/

var x = 5;      // comment
var x = 5;      /* multiline
 * comment
 */
```

Examples of **correct** code for this rule with the `{ "ignoreEOLComments": false }` (default) option:

::: correct

```js
/*eslint no-multi-spaces: ["error", { ignoreEOLComments: false }]*/

var x = 5; // comment
var x = 5; /* multiline
 * comment
 */
```

Examples of **correct** code for this rule with the `{ "ignoreEOLComments": true }` option:

::: correct

```js
/*eslint no-multi-spaces: ["error", { ignoreEOLComments: true }]*/

var x = 5; // comment
var x = 5;      // comment
var x = 5; /* multiline
 * comment
 */
var x = 5;      /* multiline
 * comment
 */
```

### exceptions

To avoid contradictions with other rules that require multiple spaces, this rule has an `exceptions` option to ignore certain nodes.

This option is an object that expects property names to be AST node types as defined by [ESTree](https://github.com/estree/estree). The easiest way to determine the node types for `exceptions` is to use [AST Explorer](https://astexplorer.net/) with the espree parser.

Only the `Property` node type is ignored by default, because for the [key-spacing](key-spacing) rule some alignment options require multiple spaces in properties of object literals.

选项 default `"exceptions": { "Property": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-multi-spaces: "error"*/
/*eslint key-spacing: ["error", { align: "value" }]*/

var obj = {
    first:  "first",
    second: "second"
};
```

选项 `"exceptions": { "Property": false }` 的 **错误** 代码示例：



```js
/*eslint no-multi-spaces: ["error", { exceptions: { "Property": false } }]*/
/*eslint key-spacing: ["error", { align: "value" }]*/

var obj = {
    first:  "first",
    second: "second"
};
```

选项 `"exceptions": { "BinaryExpression": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-multi-spaces: ["error", { exceptions: { "BinaryExpression": true } }]*/

var a = 1  *  2;
```

选项 `"exceptions": { "VariableDeclarator": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-multi-spaces: ["error", { exceptions: { "VariableDeclarator": true } }]*/

var someVar      = 'foo';
var someOtherVar = 'barBaz';
```

选项 `"exceptions": { "ImportDeclaration": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-multi-spaces: ["error", { exceptions: { "ImportDeclaration": true } }]*/

import mod          from 'mod';
import someOtherMod from 'some-other-mod';
```

## 使用建议

If you don't want to check and disallow multiple spaces, then you should turn this rule off.
