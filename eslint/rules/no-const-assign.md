---
规则名: no-const-assign
规则类型: problem
---



We cannot modify variables that are declared using `const` keyword.
It will raise a runtime error.

Under non ES2015 environment, it might be ignored merely.

## 规则详解

This rule is aimed to flag modifying variables that are declared using `const` keyword.

此规则的 **错误** 代码实例：



```js
/*eslint no-const-assign: "error"*/
/*eslint-env es6*/

const a = 0;
a = 1;
```



```js
/*eslint no-const-assign: "error"*/
/*eslint-env es6*/

const a = 0;
a += 1;
```



```js
/*eslint no-const-assign: "error"*/
/*eslint-env es6*/

const a = 0;
++a;
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-const-assign: "error"*/
/*eslint-env es6*/

const a = 0;
console.log(a);
```

::: correct

```js
/*eslint no-const-assign: "error"*/
/*eslint-env es6*/

for (const a in [1, 2, 3]) { // `a` is re-defined (not modified) on each loop step.
    console.log(a);
}
```

::: correct

```js
/*eslint no-const-assign: "error"*/
/*eslint-env es6*/

for (const a of [1, 2, 3]) { // `a` is re-defined (not modified) on each loop step.
    console.log(a);
}
```

## 禁用建议

If you don't want to be notified about modifying variables that are declared using `const` keyword, you can safely disable this rule.
