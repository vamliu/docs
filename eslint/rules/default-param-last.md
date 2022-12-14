---
规则名: default-param-last
规则类型: suggestion
---

Putting default parameter at last allows function calls to omit optional tail arguments.

```js
// Correct: optional argument can be omitted
function createUser(id, isAdmin = false) {}
createUser("tabby")

// Incorrect: optional argument can **not** be omitted
function createUser(isAdmin = false, id) {}
createUser(undefined, "tabby")
```

## 规则详解

This rule enforces default parameters to be the last of parameters.

此规则的 **错误** 代码实例：



```js
/* eslint default-param-last: ["error"] */

function f(a = 0, b) {}

function f(a, b = 0, c) {}
```

此规则的 **正确** 代码实例：

::: correct

```js
/* eslint default-param-last: ["error"] */

function f(a, b = 0) {}
```
