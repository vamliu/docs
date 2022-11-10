---
规则名: no-trailing-spaces
规则类型: layout
---



Sometimes in the course of editing files, you can end up with extra whitespace at the end of lines. These whitespace differences can be picked up by source control systems and flagged as diffs, causing frustration for developers. While this extra whitespace causes no functional issues, many code conventions require that trailing spaces be removed before check-in.

## 规则详解

This rule disallows trailing whitespace (spaces, tabs, and other Unicode whitespace characters) at the end of lines.

此规则的 **错误** 代码实例：



```js
/*eslint no-trailing-spaces: "error"*/

var foo = 0;//•••••
var baz = 5;//••
//•••••
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-trailing-spaces: "error"*/

var foo = 0;
var baz = 5;
```

## 配置项

This rule has an object option:

* `"skipBlankLines": false` (default) disallows trailing whitespace on empty lines
* `"skipBlankLines": true` allows trailing whitespace on empty lines
* `"ignoreComments": false` (default) disallows trailing whitespace in comment blocks
* `"ignoreComments": true` allows trailing whitespace in comment blocks

### skipBlankLines

选项 `{ "skipBlankLines": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-trailing-spaces: ["error", { "skipBlankLines": true }]*/

var foo = 0;
var baz = 5;
//•••••
```

### ignoreComments

选项 `{ "ignoreComments": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-trailing-spaces: ["error", { "ignoreComments": true }]*/

//foo•
//•••••
/**
 *•baz
 *••
 *•bar
 */
```
