---
规则名: no-comma-dangle

---

Disallows trailing commas in object and array literals.

(removed) This rule was **removed** in ESLint v1.0 and **replaced** by the [comma-dangle](comma-dangle) rule.

Trailing commas in object literals are valid according to the ECMAScript 5 (and ECMAScript 3!) spec, however IE8 (when not in IE8 document mode) and below will throw an error when it encounters trailing commas in JavaScript.

```js
var foo = {
    bar: "baz",
    qux: "quux",
};
```

## 规则详解

This rule is aimed at detecting trailing commas in object literals. As such, it will warn whenever it encounters a trailing comma in an object literal.

此规则的 **错误** 代码实例：



```js
var foo = {
    bar: "baz",
    qux: "quux",
};

var arr = [1,2,];

foo({
  bar: "baz",
  qux: "quux",
});
```

此规则的 **正确** 代码实例：

::: correct

```js
var foo = {
    bar: "baz",
    qux: "quux"
};

var arr = [1,2];

foo({
  bar: "baz",
  qux: "quux"
});
```

## 禁用建议

If your code will not be run in IE8 or below (a Node.js application, for example) and you'd prefer to allow trailing commas, turn this rule off.
