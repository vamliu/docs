---
规则名: space-unary-word-ops
布局: doc

---

Requires spaces after unary word operators.

(removed) This rule was **removed** in ESLint v0.10.0 and **replaced** by the [space-unary-ops](space-unary-ops) rule.

Require spaces following unary word operators.

## 规则详解

Examples of **incorrect** code for this rule:



```js
typeof!a
```



```js
void{a:0}
```



```js
new[a][0]
```



```js
delete(a.b)
```

Examples of **correct** code for this rule:

::: correct

```js
delete a.b
```

::: correct

```js
new C
```

::: correct

```js
void 0
```
