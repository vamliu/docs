---
规则名: computed-property-spacing
规则类型: layout
关联规则:
- array-bracket-spacing
- comma-spacing
- space-in-parens
---



While formatting preferences are very personal, a number of style guides require
or disallow spaces between computed properties in the following situations:

```js
/*eslint-env es6*/

var obj = { prop: "value" };
var a = "prop";
var x = obj[a]; // computed property in object member expression

var a = "prop";
var obj = {
  [a]: "value" // computed property key in object literal (ECMAScript 6)
};

var obj = { prop: "value" };
var a = "prop";
var { [a]: x } = obj; // computed property key in object destructuring pattern (ECMAScript 6)
```

## 规则详解

This rule enforces consistent spacing inside computed property brackets.

It either requires or disallows spaces between the brackets and the values inside of them.
This rule does not apply to brackets that are separated from the adjacent value by a newline.

## 配置项

This rule has two options, a string option and an object option.

String option:

* `"never"` (default) disallows spaces inside computed property brackets
* `"always"` requires one or more spaces inside computed property brackets

Object option:

* `"enforceForClassMembers": true` (default) additionally applies this rule to class members.

### never

选项 `"never"`  默认值的 **错误** 代码示例：



```js
/*eslint computed-property-spacing: ["error", "never"]*/
/*eslint-env es6*/

obj[foo ]
obj[ 'foo']
var x = {[ b ]: a}
obj[foo[ bar ]]

const { [ a ]: someProp } = obj;
({ [ b ]: anotherProp } = anotherObj);
```

选项 `"never"` 默认值的 **正确** 代码示例：

::: correct

```js
/*eslint computed-property-spacing: ["error", "never"]*/
/*eslint-env es6*/

obj[foo]
obj['foo']
var x = {[b]: a}
obj[foo[bar]]

const { [a]: someProp } = obj;
({ [b]: anotherProp } = anotherObj);
```

### always

选项 `"always"` 的 **错误** 代码示例：



```js
/*eslint computed-property-spacing: ["error", "always"]*/
/*eslint-env es6*/

obj[foo]
var x = {[b]: a}
obj[ foo]
obj['foo' ]
obj[foo[ bar ]]
var x = {[ b]: a}
const { [a]: someProp } = obj;
({ [b ]: anotherProp } = anotherObj);
```

选项 `"always"` 的 **正确** 代码示例：

::: correct

```js
/*eslint computed-property-spacing: ["error", "always"]*/
/*eslint-env es6*/

obj[ foo ]
obj[ 'foo' ]
var x = {[ b ]: a}
obj[ foo[ bar ] ]
const { [ a ]: someProp } = obj;
({ [ b ]: anotherProp } = anotherObj);
```

#### enforceForClassMembers

With `enforceForClassMembers` set to `true` (default), the rule also disallows/enforces spaces inside of computed keys of class methods, getters and setters.

Examples of **incorrect** code for this rule with `"never"` and `{ "enforceForClassMembers": true }` (default):



```js
/*eslint computed-property-spacing: ["error", "never", { "enforceForClassMembers": true }]*/
/*eslint-env es6*/

class Foo {
  [a ]() {}
  get [b ]() {}
  set [b ](value) {}
}

const Bar = class {
  [ a](){}
  static [ b]() {}
  static get [ c ]() {}
  static set [ c ](value) {}
}
```

Examples of **correct** code for this rule with `"never"` and `{ "enforceForClassMembers": true }` (default):

::: correct

```js
/*eslint computed-property-spacing: ["error", "never", { "enforceForClassMembers": true }]*/
/*eslint-env es6*/

class Foo {
  [a]() {}
  get [b]() {}
  set [b](value) {}
}

const Bar = class {
  [a](){}
  static [b]() {}
  static get [c]() {}
  static set [c](value) {}
}
```

Examples of **correct** code for this rule with `"never"` and `{ "enforceForClassMembers": false }`:

::: correct

```js
/*eslint computed-property-spacing: ["error", "never", { "enforceForClassMembers": false }]*/
/*eslint-env es6*/

class Foo {
  [a ]() {}
  get [b ]() {}
  set [b ](value) {}
}

const Bar = class {
  [ a](){}
  static [ b]() {}
  static get [ c ]() {}
  static set [ c ](value) {}
}
```

## 禁用建议

You can turn this rule off if you are not concerned with the consistency of computed properties.
