---
规则名: space-return-throw-case

---

Requires spaces after `return`, `throw`, and `case` keywords.

(removed) This rule was **removed** in ESLint v2.0 and **replaced** by the [keyword-spacing](keyword-spacing) rule.

(fixable) The `--fix` option on the [command line](../user-guide/command-line-interface#--fix) automatically fixed problems reported by this rule.

Require spaces following `return`, `throw`, and `case`.

## 规则详解

此规则的 **错误** 代码实例：



```js
/*eslint space-return-throw-case: "error"*/

throw{a:0}

function f(){ return-a; }

switch(a){ case'a': break; }
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint space-return-throw-case: "error"*/

throw {a: 0};

function f(){ return -a; }

switch(a){ case 'a': break; }
```
