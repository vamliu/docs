---
规则名: no-label-var
布局: doc
规则类型: suggestion
关联规则:
- no-extra-label
- no-labels
- no-unused-labels
---


## 规则详解

This rule aims to create clearer code by disallowing the bad practice of creating a label that shares a name with a variable that is in scope.

Examples of **incorrect** code for this rule:



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

Examples of **correct** code for this rule:

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

## 使用建议

If you don't want to be notified about usage of labels, then it's safe to disable this rule.
