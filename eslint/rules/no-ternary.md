---
规则名: no-ternary
规则类型: suggestion
关联规则:
- no-nested-ternary
- no-unneeded-ternary
---


The ternary operator is used to conditionally assign a value to a variable. Some believe that the use of ternary operators leads to unclear code.

```js
var foo = isBar ? baz : qux;
```

## 规则详解

This rule disallows ternary operators.

此规则的 **错误** 代码实例：



```js
/*eslint no-ternary: "error"*/

var foo = isBar ? baz : qux;

function quux() {
  return foo ? bar() : baz();
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-ternary: "error"*/

var foo;

if (isBar) {
    foo = baz;
} else {
    foo = qux;
}

function quux() {
    if (foo) {
        return bar();
    } else {
        return baz();
    }
}
```
