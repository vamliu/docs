---
规则名: function-paren-newline
规则类型: layout
---



Many style guides require or disallow newlines inside of function parentheses.

## 规则详解

This rule enforces consistent line breaks inside parentheses of function parameters or arguments.

### 配置项

This rule has a single option, which can either be a string or an object.

* `"always"` requires line breaks inside all function parentheses.
* `"never"` disallows line breaks inside all function parentheses.
* `"multiline"` (default) requires linebreaks inside function parentheses if any of the parameters/arguments have a line break between them. Otherwise, it disallows linebreaks.
* `"multiline-arguments"` works like `multiline` but allows linebreaks inside function parentheses if there is only one parameter/argument.
* `"consistent"` requires consistent usage of linebreaks for each pair of parentheses. It reports an error if one parenthesis in the pair has a linebreak inside it and the other parenthesis does not.
* `{ "minItems": value }` requires linebreaks inside function parentheses if the number of parameters/arguments is at least `value`. Otherwise, it disallows linebreaks.

Example configurations:

```json
{
  "rules": {
    "function-paren-newline": ["error", "never"]
  }
}
```

```json
{
  "rules": {
    "function-paren-newline": ["error", { "minItems": 3 }]
  }
}
```

选项 `"always"` 的 **错误** 代码示例：



```js
/* eslint function-paren-newline: ["error", "always"] */

function foo(bar, baz) {}

var foo = function(bar, baz) {};

var foo = (bar, baz) => {};

foo(bar, baz);
```

选项 `"always"` 的 **正确** 代码示例：

::: correct

```js
/* eslint function-paren-newline: ["error", "always"] */

function foo(
  bar,
  baz
) {}

var foo = function(
  bar, baz
) {};

var foo = (
  bar,
  baz
) => {};

foo(
  bar,
  baz
);
```

选项 `"never"` 的 **错误** 代码示例：



```js
/* eslint function-paren-newline: ["error", "never"] */

function foo(
  bar,
  baz
) {}

var foo = function(
  bar, baz
) {};

var foo = (
  bar,
  baz
) => {};

foo(
  bar,
  baz
);
```

选项 `"never"` 的 **正确** 代码示例：

::: correct

```js
/* eslint function-paren-newline: ["error", "never"] */

function foo(bar, baz) {}

function foo(bar,
             baz) {}

var foo = function(bar, baz) {};

var foo = (bar, baz) => {};

foo(bar, baz);

foo(bar,
  baz);
```

选项 `"multiline"`  默认值的 **错误** 代码示例：



```js
/* eslint function-paren-newline: ["error", "multiline"] */

function foo(bar,
  baz
) {}

var foo = function(
  bar, baz
) {};

var foo = (
  bar,
  baz) => {};

foo(bar,
  baz);

foo(
  function() {
    return baz;
  }
);
```

选项 `"multiline"` 默认值的 **正确** 代码示例：

::: correct

```js
/* eslint function-paren-newline: ["error", "multiline"] */

function foo(bar, baz) {}

var foo = function(
  bar,
  baz
) {};

var foo = (bar, baz) => {};

foo(bar, baz, qux);

foo(
  bar,
  baz,
  qux
);

foo(function() {
  return baz;
});
```

选项 `"consistent"` 的 **错误** 代码示例：



```js
/* eslint function-paren-newline: ["error", "consistent"] */

function foo(bar,
  baz
) {}

var foo = function(bar,
  baz
) {};

var foo = (
  bar,
  baz) => {};

foo(
  bar,
  baz);

foo(
  function() {
    return baz;
  });
```

选项 `"consistent"` 的 **正确** 代码示例：

::: correct

```js
/* eslint function-paren-newline: ["error", "consistent"] */

function foo(bar,
  baz) {}

var foo = function(bar, baz) {};

var foo = (
  bar,
  baz
) => {};

foo(
  bar, baz
);

foo(
  function() {
    return baz;
  }
);
```

选项 `"multiline-arguments"` 的 **错误** 代码示例：



```js
/* eslint function-paren-newline: ["error", "multiline-arguments"] */

function foo(bar,
  baz
) {}

var foo = function(bar,
  baz
) {};

var foo = (
  bar,
  baz) => {};

foo(
  bar,
  baz);

foo(
  bar, qux,
  baz
);
```

Examples of **correct** code for this rule with the consistent `"multiline-arguments"` option:

::: correct

```js
/* eslint function-paren-newline: ["error", "multiline-arguments"] */

function foo(
  bar,
  baz
) {}

var foo = function(bar, baz) {};

var foo = (
  bar
) => {};

foo(
  function() {
    return baz;
  }
);
```

选项 `{ "minItems": 3 }` 的 **错误** 代码示例：



```js
/* eslint function-paren-newline: ["error", { "minItems": 3 }] */

function foo(
  bar,
  baz
) {}

function foo(bar, baz, qux) {}

var foo = function(
  bar, baz
) {};

var foo = (bar,
  baz) => {};

foo(bar,
  baz);
```

选项 `{ "minItems": 3 }` 的 **正确** 代码示例：

::: correct

```js
/* eslint function-paren-newline: ["error", { "minItems": 3 }] */

function foo(bar, baz) {}

var foo = function(
  bar,
  baz,
  qux
) {};

var foo = (
  bar, baz, qux
) => {};

foo(bar, baz);

foo(
  bar, baz, qux
);
```

## 禁用建议

If don't want to enforce consistent linebreaks inside function parentheses, do not turn on this rule.
