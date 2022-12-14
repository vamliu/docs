---
规则名: no-regex-spaces
规则类型: suggestion
关联规则:
- no-div-regex
- no-control-regex
---





Regular expressions can be very complex and difficult to understand, which is why it's important to keep them as simple as possible in order to avoid mistakes. One of the more error-prone things you can do with a regular expression is to use more than one space, such as:

```js
var re = /foo   bar/;
```

In this regular expression, it's very hard to tell how many spaces are intended to be matched. It's better to use only one space and then specify how many spaces are expected, such as:

```js
var re = /foo {3}bar/;
```

Now it is very clear that three spaces are expected to be matched.

## 规则详解

This rule disallows multiple spaces in regular expression literals.

此规则的 **错误** 代码实例：



```js
/*eslint no-regex-spaces: "error"*/

var re = /foo   bar/;
var re = new RegExp("foo   bar");
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-regex-spaces: "error"*/

var re = /foo {3}bar/;
var re = new RegExp("foo {3}bar");
```

## 禁用建议

If you want to allow multiple spaces in a regular expression, then you can safely turn this rule off.
