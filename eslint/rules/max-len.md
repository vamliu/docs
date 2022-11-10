---
规则名: max-len
规则类型: layout
关联规则:
- complexity
- max-depth
- max-nested-callbacks
- max-params
- max-statements
---


Very long lines of code in any language can be difficult to read. In order to aid in readability and maintainability many coders have developed a convention to limit lines of code to X number of characters (traditionally 80 characters).

```js
var foo = { "bar": "This is a bar.", "baz": { "qux": "This is a qux" }, "difficult": "to read" }; // very long
```

## 规则详解

This rule enforces a maximum line length to increase code readability and maintainability. The length of a line is defined as the number of Unicode characters in the line.

## 配置项

This rule has a number or object option:

* `"code"` (default `80`) enforces a maximum line length
* `"tabWidth"` (default `4`) specifies the character width for tab characters
* `"comments"` enforces a maximum line length for comments; defaults to value of `code`
* `"ignorePattern"` ignores lines matching a regular expression; can only match a single line and need to be double escaped when written in YAML or JSON
* `"ignoreComments": true` ignores all trailing comments and comments on their own line
* `"ignoreTrailingComments": true` ignores only trailing comments
* `"ignoreUrls": true` ignores lines that contain a URL
* `"ignoreStrings": true` ignores lines that contain a double-quoted or single-quoted string
* `"ignoreTemplateLiterals": true` ignores lines that contain a template literal
* `"ignoreRegExpLiterals": true` ignores lines that contain a RegExp literal

### code

选项 `{ "code": 80 }`  默认值的 **错误** 代码示例：



```js
/*eslint max-len: ["error", { "code": 80 }]*/

var foo = { "bar": "This is a bar.", "baz": { "qux": "This is a qux" }, "difficult": "to read" };
```

选项 `{ "code": 80 }` 默认值的 **正确** 代码示例：

::: correct

```js
/*eslint max-len: ["error", { "code": 80 }]*/

var foo = {
  "bar": "This is a bar.",
  "baz": { "qux": "This is a qux" },
  "easier": "to read"
};
```

### tabWidth

选项 `{ "tabWidth": 4 }`  默认值的 **错误** 代码示例：



```js
/*eslint max-len: ["error", { "code": 80, "tabWidth": 4 }]*/

\t  \t  var foo = { "bar": "This is a bar.", "baz": { "qux": "This is a qux" } };
```

选项 `{ "tabWidth": 4 }` 默认值的 **正确** 代码示例：

::: correct

```js
/*eslint max-len: ["error", { "code": 80, "tabWidth": 4 }]*/

\t  \t  var foo = {
\t  \t  \t  \t  "bar": "This is a bar.",
\t  \t  \t  \t  "baz": { "qux": "This is a qux" }
\t  \t  };
```

### comments

选项 `{ "comments": 65 }` 的 **错误** 代码示例：



```js
/*eslint max-len: ["error", { "comments": 65 }]*/

/**
 * This is a comment that violates the maximum line length we have specified
**/
```

### ignoreComments

选项 `{ "ignoreComments": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint max-len: ["error", { "ignoreComments": true }]*/

/**
 * This is a really really really really really really really really really long comment
**/
```

### ignoreTrailingComments

选项 `{ "ignoreTrailingComments": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint max-len: ["error", { "ignoreTrailingComments": true }]*/

var foo = 'bar'; // This is a really really really really really really really long comment
```

### ignoreUrls

选项 `{ "ignoreUrls": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint max-len: ["error", { "ignoreUrls": true }]*/

var url = 'https://www.example.com/really/really/really/really/really/really/really/long';
```

### ignoreStrings

选项 `{ "ignoreStrings": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint max-len: ["error", { "ignoreStrings": true }]*/

var longString = 'this is a really really really really really long string!';
```

### ignoreTemplateLiterals

选项 `{ "ignoreTemplateLiterals": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint max-len: ["error", { "ignoreTemplateLiterals": true }]*/

var longTemplateLiteral = `this is a really really really really really long template literal!`;
```

### ignoreRegExpLiterals

选项 `{ "ignoreRegExpLiterals": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint max-len: ["error", { "ignoreRegExpLiterals": true }]*/

var longRegExpLiteral = /this is a really really really really really long regular expression!/;
```

### ignorePattern

选项 `ignorePattern` 的 **正确** 代码示例：

::: correct

```js
/*eslint max-len: ["error", { "ignorePattern": "^\\s*var\\s.+=\\s*require\\s*\\(" }]*/

var dep = require('really/really/really/really/really/really/really/really/long/module');
```
