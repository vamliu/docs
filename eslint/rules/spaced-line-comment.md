---
规则名: spaced-line-comment

关联规则:
- spaced-comment
---

Enforces consistent spacing after `//` in line comments.

(removed) This rule was **removed** in ESLint v1.0 and **replaced** by the [spaced-comment](spaced-comment) rule.

Some style guides require or disallow a whitespace immediately after the initial `//` of a line comment.
Whitespace after the `//` makes it easier to read text in comments.
On the other hand, commenting out code is easier without having to put a whitespace right after the `//`.

## 规则详解

This rule will enforce consistency of spacing after the start of a line comment `//`.

This rule takes two arguments. If the first is `"always"` then the `//` must be followed by at least once whitespace.
If `"never"` then there should be no whitespace following.
The default is `"always"`.

The second argument is an object with one key, `"exceptions"`.
The value is an array of string patterns which are considered exceptions to the rule.
It is important to note that the exceptions are ignored if the first argument is `"never"`.
Exceptions cannot be mixed.

此规则的 **错误** 代码实例：



```js
// When ["never"]
// This is a comment with a whitespace at the beginning
```



```js
//When ["always"]
//This is a comment with no whitespace at the beginning
var foo = 5;
```



```js
// When ["always",{"exceptions":["-","+"]}]
//------++++++++
// Comment block
//------++++++++
```

此规则的 **正确** 代码实例：

::: correct

```js
// When ["always"]
// This is a comment with a whitespace at the beginning
var foo = 5;
```

::: correct

```js
//When ["never"]
//This is a comment with no whitespace at the beginning
var foo = 5;
```

::: correct

```js
// When ["always",{"exceptions":["-"]}]
//--------------
// Comment block
//--------------
```

::: correct

```js
// When ["always",{"exceptions":["-+"]}]
//-+-+-+-+-+-+-+
// Comment block
//-+-+-+-+-+-+-+
```
