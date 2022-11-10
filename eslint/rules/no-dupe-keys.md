---
规则名: no-dupe-keys
规则类型: problem
---



Multiple properties with the same key in object literals can cause unexpected behavior in your application.

```js
var foo = {
    bar: "baz",
    bar: "qux"
};
```

## 规则详解

This rule disallows duplicate keys in object literals.

此规则的 **错误** 代码实例：



```js
/*eslint no-dupe-keys: "error"*/

var foo = {
    bar: "baz",
    bar: "qux"
};

var foo = {
    "bar": "baz",
    bar: "qux"
};

var foo = {
    0x1: "baz",
    1: "qux"
};
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-dupe-keys: "error"*/

var foo = {
    bar: "baz",
    quxx: "qux"
};
```
