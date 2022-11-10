---
规则名: space-unary-word-ops

---

Requires spaces after unary word operators.

(removed) This rule was **removed** in ESLint v0.10.0 and **replaced** by the [space-unary-ops](space-unary-ops) rule.

Require spaces following unary word operators.

## 规则详解

此规则的 **错误** 代码实例：



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

此规则的 **正确** 代码实例：

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
