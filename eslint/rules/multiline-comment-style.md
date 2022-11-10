---
规则名: multiline-comment-style
规则类型: suggestion
---



Many style guides require a particular style for comments that span multiple lines. For example, some style guides prefer the use of a single block comment for multiline comments, whereas other style guides prefer consecutive line comments.

## 规则详解

This rule aims to enforce a particular style for multiline comments.

### 配置项

This rule has a string option, which can have one of the following values:

* `"starred-block"` (default): Disallows consecutive line comments in favor of block comments. Additionally, requires block comments to have an aligned `*` character before each line.
* `"bare-block"`: Disallows consecutive line comments in favor of block comments, and disallows block comments from having a `"*"` character before each line.
* `"separate-lines"`: Disallows block comments in favor of consecutive line comments

The rule always ignores directive comments such as `/* eslint-disable */`. Additionally, unless the mode is `"starred-block"`, the rule ignores JSDoc comments.

选项 `"starred-block"`  默认值的 **错误** 代码示例：



```js

/* eslint multiline-comment-style: ["error", "starred-block"] */

// this line
// calls foo()
foo();

/* this line
calls foo() */
foo();

/* this comment
 * is missing a newline after /*
 */

/*
 * this comment
 * is missing a newline at the end */

/*
* the star in this line should have a space before it
 */

/*
 * the star on the following line should have a space before it
*/

```

选项 `"starred-block"` 默认值的 **正确** 代码示例：

::: correct

```js
/* eslint multiline-comment-style: ["error", "starred-block"] */

/*
 * this line
 * calls foo()
 */
foo();

// single-line comment
```

选项 `"bare-block"` 的 **错误** 代码示例：



```js
/* eslint multiline-comment-style: ["error", "bare-block"] */

// this line
// calls foo()
foo();

/*
 * this line
 * calls foo()
 */
foo();
```

选项 `"bare-block"` 的 **正确** 代码示例：

::: correct

```js
/* eslint multiline-comment-style: ["error", "bare-block"] */

/* this line
   calls foo() */
foo();
```

选项 `"separate-lines"` 的 **错误** 代码示例：



```js

/* eslint multiline-comment-style: ["error", "separate-lines"] */

/* This line
calls foo() */
foo();

/*
 * This line
 * calls foo()
 */
foo();

```

选项 `"separate-lines"` 的 **正确** 代码示例：

::: correct

```js
/* eslint multiline-comment-style: ["error", "separate-lines"] */

// This line
// calls foo()
foo();

```

## 禁用建议

If you don't want to enforce a particular style for multiline comments, you can disable the rule.
