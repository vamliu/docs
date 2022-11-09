---
规则名: no-div-regex
布局: doc
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

Examples of **incorrect** code for this rule:

```js
/*eslint no-div-regex: "error"*/

function bar() { return /=foo/; }
```

Examples of **correct** code for this rule:

```js
/*eslint no-div-regex: "error"*/

function bar() { return /[=]foo/; }
```
