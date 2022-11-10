---
规则名: line-comment-position
规则类型: layout
---


Line comments can be positioned above or beside code. This rule helps teams maintain a consistent style.

```js
// above comment
var foo = "bar";  // beside comment
```

## 规则详解

This rule enforces consistent position of line comments. Block comments are not affected by this rule. By default, this rule ignores comments starting with the following words: `eslint`, `jshint`, `jslint`, `istanbul`, `global`, `exported`, `jscs`, `falls through`.

## 配置项

This rule takes one argument, which can be a string or an object. The string settings are the same as those of the `position` property (explained below). The object option has the following properties:

### position

The `position` option has two settings:

* `above` (default) enforces line comments only above code, in its own line.
* `beside` enforces line comments only at the end of code lines.

#### position: above

选项 `{ "position": "above" }` 的 **正确** 代码示例：

::: correct

```js
/*eslint line-comment-position: ["error", { "position": "above" }]*/
// valid comment
1 + 1;
```

选项 `{ "position": "above" }` 的 **错误** 代码示例：



```js
/*eslint line-comment-position: ["error", { "position": "above" }]*/
1 + 1; // invalid comment
```

#### position: beside

选项 `{ "position": "beside" }` 的 **正确** 代码示例：

::: correct

```js
/*eslint line-comment-position: ["error", { "position": "beside" }]*/
1 + 1; // valid comment
```

选项 `{ "position": "beside" }` 的 **错误** 代码示例：



```js
/*eslint line-comment-position: ["error", { "position": "beside" }]*/
// invalid comment
1 + 1;
```

### ignorePattern

By default this rule ignores comments starting with the following words: `eslint`, `jshint`, `jslint`, `istanbul`, `global`, `exported`, `jscs`, `falls through`. An alternative regular expression can be provided.

选项 `ignorePattern` 的 **正确** 代码示例：

::: correct

```js
/*eslint line-comment-position: ["error", { "ignorePattern": "pragma" }]*/
1 + 1; // pragma valid comment
```

选项 `ignorePattern` 的 **错误** 代码示例：



```js
/*eslint line-comment-position: ["error", { "ignorePattern": "pragma" }]*/
1 + 1; // invalid comment
```

### applyDefaultIgnorePatterns

Default ignore patterns are applied even when `ignorePattern` is provided. If you want to omit default patterns, set this option to `false`.

选项 `{ "applyDefaultIgnorePatterns": false }` 的 **正确** 代码示例：

::: correct

```js
/*eslint line-comment-position: ["error", { "ignorePattern": "pragma", "applyDefaultIgnorePatterns": false }]*/
1 + 1; // pragma valid comment
```

选项 `{ "applyDefaultIgnorePatterns": false }` 的 **错误** 代码示例：



```js
/*eslint line-comment-position: ["error", { "ignorePattern": "pragma", "applyDefaultIgnorePatterns": false }]*/
1 + 1; // falls through
```

**Deprecated:** the object property `applyDefaultPatterns` is deprecated. Please use the property `applyDefaultIgnorePatterns` instead.

## 禁用建议

If you aren't concerned about having different line comment styles, then you can turn off this rule.

## 兼容

**JSCS**: [validateCommentPosition](https://jscs-dev.github.io/rule/validateCommentPosition)
