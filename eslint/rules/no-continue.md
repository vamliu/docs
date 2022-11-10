---
规则名: no-continue
规则类型: suggestion
---


The `continue` statement terminates execution of the statements in the current iteration of the current or labeled loop, and continues execution of the loop with the next iteration. When used incorrectly it makes code less testable, less readable and less maintainable. Structured control flow statements such as `if` should be used instead.

```js
var sum = 0,
    i;

for(i = 0; i < 10; i++) {
    if(i >= 5) {
        continue;
    }

    a += i;
}
```

## 规则详解

This rule disallows `continue` statements.

此规则的 **错误** 代码实例：



```js
/*eslint no-continue: "error"*/

var sum = 0,
    i;

for(i = 0; i < 10; i++) {
    if(i >= 5) {
        continue;
    }

    a += i;
}
```



```js
/*eslint no-continue: "error"*/

var sum = 0,
    i;

labeledLoop: for(i = 0; i < 10; i++) {
    if(i >= 5) {
        continue labeledLoop;
    }

    a += i;
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-continue: "error"*/

var sum = 0,
    i;

for(i = 0; i < 10; i++) {
    if(i < 5) {
       a += i;
    }
}
```

## 兼容

* **JSLint**: `continue`
