---
规则名: max-params
规则类型: suggestion
关联规则:
- complexity
- max-depth
- max-len
- max-lines
- max-lines-per-function
- max-nested-callbacks
- max-statements
---


Functions that take numerous parameters can be difficult to read and write because it requires the memorization of what each parameter is, its type, and the order they should appear in. As a result, many coders adhere to a convention that caps the number of parameters a function can take.

```js
function foo (bar, baz, qux, qxx) { // four parameters, may be too many
    doSomething();
}
```

## 规则详解

This rule enforces a maximum number of parameters allowed in function definitions.

## 配置项

This rule has a number or object option:

* `"max"` (default `3`) enforces a maximum number of parameters in function definitions

**Deprecated:** The object property `maximum` is deprecated; please use the object property `max` instead.

### max

选项 `{ "max": 3 }`  默认值的 **错误** 代码示例：

```js
/*eslint max-params: ["error", 3]*/
/*eslint-env es6*/

function foo (bar, baz, qux, qxx) {
    doSomething();
}

let foo = (bar, baz, qux, qxx) => {
    doSomething();
};
```

选项 `{ "max": 3 }` 默认值的 **正确** 代码示例：

```js
/*eslint max-params: ["error", 3]*/
/*eslint-env es6*/

function foo (bar, baz, qux) {
    doSomething();
}

let foo = (bar, baz, qux) => {
    doSomething();
};
```
