---
规则名: no-extra-label
规则类型: suggestion
关联规则:
- no-labels
- no-label-var
- no-unused-labels
---



If a loop contains no nested loops or switches, labeling the loop is unnecessary.

```js
A: while (a) {
    break A;
}
```

You can achieve the same result by removing the label and using `break` or `continue` without a label.
Probably those labels would confuse developers because they expect labels to jump to further.

## 规则详解

This rule is aimed at eliminating unnecessary labels.

此规则的 **错误** 代码实例：



```js
/*eslint no-extra-label: "error"*/

A: while (a) {
    break A;
}

B: for (let i = 0; i < 10; ++i) {
    break B;
}

C: switch (a) {
    case 0:
        break C;
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-extra-label: "error"*/

while (a) {
    break;
}

for (let i = 0; i < 10; ++i) {
    break;
}

switch (a) {
    case 0:
        break;
}

A: {
    break A;
}

B: while (a) {
    while (b) {
        break B;
    }
}

C: switch (a) {
    case 0:
        while (b) {
            break C;
        }
        break;
}
```

## 禁用建议

If you don't want to be notified about usage of labels, then it's safe to disable this rule.
