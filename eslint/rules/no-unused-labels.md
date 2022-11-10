---
规则名: no-unused-labels
规则类型: suggestion
关联规则:
- no-extra-label
- no-labels
- no-label-var
---





Labels that are declared and not used anywhere in the code are most likely an error due to incomplete refactoring.

```js
OUTER_LOOP:
for (const student of students) {
    if (checkScores(student.scores)) {
        continue;
    }
    doSomething(student);
}
```

In this case, probably removing `OUTER_LOOP:` had been forgotten.
Such labels take up space in the code and can lead to confusion by readers.

## 规则详解

This rule is aimed at eliminating unused labels.

此规则的 **错误** 代码实例：



```js
/*eslint no-unused-labels: "error"*/

A: var foo = 0;

B: {
    foo();
}

C:
for (let i = 0; i < 10; ++i) {
    foo();
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-unused-labels: "error"*/

A: {
    if (foo()) {
        break A;
    }
    bar();
}

B:
for (let i = 0; i < 10; ++i) {
    if (foo()) {
        break B;
    }
    bar();
}
```

## 禁用建议

If you don't want to be notified about unused labels, then it's safe to disable this rule.
