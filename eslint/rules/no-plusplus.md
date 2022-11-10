---
规则名: no-plusplus
规则类型: suggestion
---


Because the unary `++` and `--` operators are subject to automatic semicolon insertion, differences in whitespace can change semantics of source code.

```js
var i = 10;
var j = 20;

i ++
j
// i = 11, j = 20
```

```js
var i = 10;
var j = 20;

i
++
j
// i = 10, j = 21
```

## 规则详解

This rule disallows the unary operators `++` and `--`.

此规则的 **错误** 代码实例：



```js
/*eslint no-plusplus: "error"*/

var foo = 0;
foo++;

var bar = 42;
bar--;

for (i = 0; i < l; i++) {
    return;
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-plusplus: "error"*/

var foo = 0;
foo += 1;

var bar = 42;
bar -= 1;

for (i = 0; i < l; i += 1) {
    return;
}
```

## 配置项

This rule has an object option.

* `"allowForLoopAfterthoughts": true` allows unary operators `++` and `--` in the afterthought (final expression) of a `for` loop.

### allowForLoopAfterthoughts

选项 `{ "allowForLoopAfterthoughts": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-plusplus: ["error", { "allowForLoopAfterthoughts": true }]*/

for (i = 0; i < l; i++) {
    doSomething(i);
}

for (i = l; i >= 0; i--) {
    doSomething(i);
}

for (i = 0, j = l; i < l; i++, j--) {
    doSomething(i, j);
}
```

选项 `{ "allowForLoopAfterthoughts": true }` 的 **错误** 代码示例：



```js
/*eslint no-plusplus: ["error", { "allowForLoopAfterthoughts": true }]*/

for (i = 0; i < l; j = i++) {
    doSomething(i, j);
}

for (i = l; i--;) {
    doSomething(i);
}

for (i = 0; i < l;) i++;
```
