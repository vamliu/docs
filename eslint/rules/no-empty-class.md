---
规则名: no-empty-class

---

Disallows empty character classes in regular expressions.

(removed) This rule was **removed** in ESLint v1.0 and **replaced** by the [no-empty-character-class](no-empty-character-class) rule.

Empty character classes in regular expressions do not match anything and can result in code that may not work as intended.

```js
var foo = /^abc[]/;
```

## 规则详解

This rule is aimed at highlighting possible typos and unexpected behavior in regular expressions which may arise from the use of empty character classes.

此规则的 **错误** 代码实例：



```js
var foo = /^abc[]/;

/^abc[]/.test(foo);

bar.match(/^abc[]/);
```

此规则的 **正确** 代码实例：

::: correct

```js
var foo = /^abc/;

var foo = /^abc[a-z]/;

var bar = new RegExp("^abc[]");
```
