---
规则名: no-global-assign
布局: doc
规则类型: suggestion
关联规则:
- no-extend-native
- no-redeclare
- no-shadow
---



JavaScript environments contain a number of built-in global variables, such as `window` in browsers and `process` in Node.js. In almost all cases, you don't want to assign a value to these global variables as doing so could result in losing access to important functionality. For example, you probably don't want to do this in browser code:

```js
window = {};
```

While examples such as `window` are obvious, there are often hundreds of built-in global objects provided by JavaScript environments. It can be hard to know if you're assigning to a global variable or not.

## 规则详解

This rule disallows modifications to read-only global variables.

ESLint has the capability to configure global variables as read-only.

* [Specifying Environments](../user-guide/configuring#specifying-environments)
* [Specifying Globals](../user-guide/configuring#specifying-globals)

Examples of **incorrect** code for this rule:



```js
/*eslint no-global-assign: "error"*/

Object = null
undefined = 1
```



```js
/*eslint no-global-assign: "error"*/
/*eslint-env browser*/

window = {}
length = 1
top = 1
```



```js
/*eslint no-global-assign: "error"*/
/*global a:readonly*/

a = 1
```

Examples of **correct** code for this rule:

::: correct

```js
/*eslint no-global-assign: "error"*/

a = 1
var b = 1
b = 2
```

::: correct

```js
/*eslint no-global-assign: "error"*/
/*eslint-env browser*/

onload = function() {}
```

::: correct

```js
/*eslint no-global-assign: "error"*/
/*global a:writable*/

a = 1
```

## 配置项

This rule accepts an `exceptions` option, which can be used to specify a list of builtins for which reassignments will be allowed:

```json
{
    "rules": {
        "no-global-assign": ["error", {"exceptions": ["Object"]}]
    }
}
```

## 使用建议

If you are trying to override one of the native objects.
