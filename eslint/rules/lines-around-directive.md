---
规则名: lines-around-directive
规则类型: layout
关联规则:
- lines-around-comment
- padded-blocks
---



This rule was **deprecated** in ESLint v4.0.0 and replaced by the [padding-line-between-statements](padding-line-between-statements) rule.

Directives are used in JavaScript to indicate to the execution environment that a script would like to opt into a feature such as `"strict mode"`. Directives are grouped together in a [directive prologue](https://www.ecma-international.org/ecma-262/7.0/#directive-prologue) at the top of either a file or function block and are applied to the scope in which they occur.

```js
// Strict mode is invoked for the entire script
"use strict";

var foo;

function bar() {
  var baz;
}
```

```js
var foo;

function bar() {
  // Strict mode is only invoked within this function
  "use strict";

  var baz;
}
```

## 规则详解

This rule requires or disallows blank newlines around directive prologues. This rule does not enforce any conventions about blank newlines between the individual directives. In addition, it does not require blank newlines before directive prologues unless they are preceded by a comment. Please use the [padded-blocks](padded-blocks) rule if this is a style you would like to enforce.

## 配置项

This rule has one option. It can either be a string or an object:

* `"always"` (default) enforces blank newlines around directives.
* `"never"` disallows blank newlines around directives.

or

```js
{
  "before": "always" or "never"
  "after": "always" or "never",
}
```

### always

This is the default option.

选项 `"always"` 的 **错误** 代码示例：



```js
/* eslint lines-around-directive: ["error", "always"] */

/* Top of file */
"use strict";
var foo;

/* Top of file */
// comment
"use strict";
"use asm";
var foo;

function foo() {
  "use strict";
  "use asm";
  var bar;
}

function foo() {
  // comment
  "use strict";
  var bar;
}
```

选项 `"always"` 的 **正确** 代码示例：

::: correct

```js
/* eslint lines-around-directive: ["error", "always"] */

/* Top of file */
"use strict";

var foo;

/* Top of file */
// comment

"use strict";
"use asm";

var foo;

function foo() {
  "use strict";
  "use asm";

  var bar;
}

function foo() {
  // comment

  "use strict";

  var bar;
}
```

### never

选项 `"never"` 的 **错误** 代码示例：



```js
/* eslint lines-around-directive: ["error", "never"] */

/* Top of file */

"use strict";

var foo;

/* Top of file */
// comment

"use strict";
"use asm";

var foo;

function foo() {
  "use strict";
  "use asm";

  var bar;
}

function foo() {
  // comment

  "use strict";

  var bar;
}
```

选项 `"never"` 的 **正确** 代码示例：

::: correct

```js
/* eslint lines-around-directive: ["error", "never"] */

/* Top of file */
"use strict";
var foo;

/* Top of file */
// comment
"use strict";
"use asm";
var foo;

function foo() {
  "use strict";
  "use asm";
  var bar;
}

function foo() {
  // comment
  "use strict";
  var bar;
}
```

### before & after

选项 `{ "before": "never", "after": "always" }` 的 **错误** 代码示例：



```js
/* eslint lines-around-directive: ["error", { "before": "never", "after": "always" }] */

/* Top of file */

"use strict";
var foo;

/* Top of file */
// comment

"use strict";
"use asm";
var foo;

function foo() {
  "use strict";
  "use asm";
  var bar;
}

function foo() {
  // comment

  "use strict";
  var bar;
}
```

选项 `{ "before": "never", "after": "always" }`   的 **正确** 代码示例

::: correct

```js
/* eslint lines-around-directive: ["error", { "before": "never", "after": "always" }] */

/* Top of file */
"use strict";

var foo;

/* Top of file */
// comment
"use strict";
"use asm";

var foo;

function foo() {
  "use strict";
  "use asm";

  var bar;
}

function foo() {
  // comment
  "use strict";

  var bar;
}
```

选项 `{ "before": "always", "after": "never" }` 的 **错误** 代码示例：



```js
/* eslint lines-around-directive: ["error", { "before": "always", "after": "never" }] */

/* Top of file */
"use strict";

var foo;

/* Top of file */
// comment
"use strict";
"use asm";

var foo;

function foo() {
  "use strict";
  "use asm";

  var bar;
}

function foo() {
  // comment
  "use strict";

  var bar;
}
```

选项 `{ "before": "always", "after": "never" }` 的 **正确** 代码示例：

::: correct

```js
/* eslint lines-around-directive: ["error", { "before": "always", "after": "never" }] */

/* Top of file */
"use strict";
var foo;

/* Top of file */
// comment

"use strict";
"use asm";
var foo;

function foo() {
  "use strict";
  "use asm";
  var bar;
}

function foo() {
  // comment

  "use strict";
  var bar;
}
```

## 禁用建议

You can safely disable this rule if you do not have any strict conventions about whether or not directive prologues should have blank newlines before or after them.

## 兼容

* **JSCS**: [requirePaddingNewLinesAfterUseStrict](https://jscs-dev.github.io/rule/requirePaddingNewLinesAfterUseStrict)
* **JSCS**: [disallowPaddingNewLinesAfterUseStrict](https://jscs-dev.github.io/rule/disallowPaddingNewLinesAfterUseStrict)
