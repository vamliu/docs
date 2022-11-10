---
规则名: no-label-var
规则类型: suggestion
关联规则:
- no-extra-label
- no-labels
- no-unused-labels
---


## 规则详解

This rule aims to create clearer code by disallowing the bad practice of creating a label that shares a name with a variable that is in scope.

此规则的 **错误** 代码实例：



```js
/*eslint no-label-var: "error"*/

var x = foo;
function bar() {
x:
  for (;;) {
    break x;
  }
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-label-var: "error"*/

// The variable that has the same name as the label is not in scope.

function foo() {
  var q = t;
}

function bar() {
q:
  for(;;) {
    break q;
  }
}
```

## 禁用建议

If you don't want to be notified about usage of labels, then it's safe to disable this rule.
