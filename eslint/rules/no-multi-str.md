---
规则名: no-multi-str
规则类型: suggestion
---


It's possible to create multiline strings in JavaScript by using a slash before a newline, such as:

```js
var x = "Line 1 \
         Line 2";
```

Some consider this to be a bad practice as it was an undocumented feature of JavaScript that was only formalized later.

## 规则详解

This rule is aimed at preventing the use of multiline strings.

此规则的 **错误** 代码实例：



```js
/*eslint no-multi-str: "error"*/

var x = "some very \
long text";
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-multi-str: "error"*/

var x = "some very long text";

var x = "some very " +
        "long text";
```
