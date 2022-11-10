---
规则名: no-div-regex
规则类型: suggestion
关联规则:
- no-control-regex
- no-regex-spaces
---



Require regex literals to escape division operators.

```js
function bar() { return /=foo/; }
```

## 规则详解

This is used to disambiguate the division operator to not confuse users.

此规则的 **错误** 代码实例：

```js
/*eslint no-div-regex: "error"*/

function bar() { return /=foo/; }
```

此规则的 **正确** 代码实例：

```js
/*eslint no-div-regex: "error"*/

function bar() { return /[=]foo/; }
```
