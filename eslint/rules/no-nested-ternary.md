---
规则名: no-nested-ternary
规则类型: suggestion
关联规则:
- no-ternary
- no-unneeded-ternary
---


Nesting ternary expressions can make code more difficult to understand.

```js
var foo = bar ? baz : qux === quxx ? bing : bam;
```

## 规则详解

The `no-nested-ternary` rule disallows nested ternary expressions.

此规则的 **错误** 代码实例：



```js
/*eslint no-nested-ternary: "error"*/

var thing = foo ? bar : baz === qux ? quxx : foobar;

foo ? baz === qux ? quxx() : foobar() : bar();
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-nested-ternary: "error"*/

var thing = foo ? bar : foobar;

var thing;

if (foo) {
  thing = bar;
} else if (baz === qux) {
  thing = quxx;
} else {
  thing = foobar;
}
```
