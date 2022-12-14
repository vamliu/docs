---
规则名: wrap-regex
规则类型: layout
---



When a regular expression is used in certain situations, it can end up looking like a division operator. For example:

```js
function a() {
    return /foo/.test("bar");
}
```

## 规则详解

This is used to disambiguate the slash operator and facilitates more readable code.

Example of **incorrect** code for this rule:



```js
/*eslint wrap-regex: "error"*/

function a() {
    return /foo/.test("bar");
}
```

Example of **correct** code for this rule:

::: correct

```js
/*eslint wrap-regex: "error"*/

function a() {
    return (/foo/).test("bar");
}
```
