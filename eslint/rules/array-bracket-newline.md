---
规则名: array-bracket-newline
规则类型: layout
关联规则:
- array-bracket-spacing
---

许多样式规范都限制了是否使用数组括号内的换行符。

## 规则详解

此规则在左括号之后和数组右括号之前强制换行。

## 配置项

此规则有一个字符串选项：
This rule has either a string option:

* `"always"` 括号内需要换行
* `"never"` 括号内不允许换行
* `"consistent"` 要求对每对括号使用一致的换行符。如果一对括号中的一个括号内有换行符而另一个括号中没有换行符，则会触发警告。

也可以配置一个对象选项（如果满足任何属性，则需要换行。否则，不允许换行）：

* `"multiline": true` （默认值）如果元素内部或元素之间存在换行符，则需要换行符。如果为false，则禁用此条件。
* `"minItems": null` （默认值）如果元素数至少为给定整数，则需要换行。如果该值为0，则该条件的作用与选项 `"always"` 相同。如果此值为 `null`（默认值），则禁用此条件。

### always

选项 `"always"` 的 **错误** 代码示例：

```js
/*eslint array-bracket-newline: ["error", "always"]*/

var a = [];
var b = [1];
var c = [1, 2];
var d = [1,
    2];
var e = [function foo() {
    dosomething();
}];
```

选项 `"always"` 的 **正确** 代码示例：

```js
/*eslint array-bracket-newline: ["error", "always"]*/

var a = [
];
var b = [
    1
];
var c = [
    1, 2
];
var d = [
    1,
    2
];
var e = [
    function foo() {
        dosomething();
    }
];
```

### never

选项 `"never"` 的 **错误** 代码示例：

```js
/*eslint array-bracket-newline: ["error", "never"]*/

var a = [
];
var b = [
    1
];
var c = [
    1, 2
];
var d = [
    1,
    2
];
var e = [
    function foo() {
        dosomething();
    }
];
```

选项 `"never"` 的 **正确** 代码示例：

```js
/*eslint array-bracket-newline: ["error", "never"]*/

var a = [];
var b = [1];
var c = [1, 2];
var d = [1,
    2];
var e = [function foo() {
    dosomething();
}];
```

### consistent

选项 `"consistent"` 的 **错误** 代码示例：

```js
/*eslint array-bracket-newline: ["error", "consistent"]*/

var a = [1
];
var b = [
    1];
var c = [function foo() {
    dosomething();
}
]
var d = [
    function foo() {
        dosomething();
    }]
```

选项 `"consistent"` 的 **正确** 代码示例：

```js
/*eslint array-bracket-newline: ["error", "consistent"]*/

var a = [];
var b = [
];
var c = [1];
var d = [
    1
];
var e = [function foo() {
    dosomething();
}];
var f = [
    function foo() {
        dosomething();
    }
];
```

### multiline

选项 `{ "multiline": true }`  默认值的 **错误** 代码示例：

```js
/*eslint array-bracket-newline: ["error", { "multiline": true }]*/

var a = [
];
var b = [
    1
];
var c = [
    1, 2
];
var d = [1,
    2];
var e = [function foo() {
    dosomething();
}];
```

选项 `{ "multiline": true }` 默认值的 **正确** 代码示例：

```js
/*eslint array-bracket-newline: ["error", { "multiline": true }]*/

var a = [];
var b = [1];
var c = [1, 2];
var d = [
    1,
    2
];
var e = [
    function foo() {
        dosomething();
    }
];
```

### minItems

选项 `{ "minItems": 2 }` 的 **错误** 代码示例：

```js
/*eslint array-bracket-newline: ["error", { "minItems": 2 }]*/

var a = [
];
var b = [
    1
];
var c = [1, 2];
var d = [1,
    2];
var e = [
  function foo() {
    dosomething();
  }
];
```

选项 `{ "minItems": 2 }` 的 **正确** 代码示例：

```js
/*eslint array-bracket-newline: ["error", { "minItems": 2 }]*/

var a = [];
var b = [1];
var c = [
    1, 2
];
var d = [
    1,
    2
];
var e = [function foo() {
    dosomething();
}];
```

### multiline and minItems

选项 `{ "multiline": true, "minItems": 2 }`  的 **错误** 代码示例：

```js
/*eslint array-bracket-newline: ["error", { "multiline": true, "minItems": 2 }]*/

var a = [
];
var b = [
    1
];
var c = [1, 2];
var d = [1,
    2];
var e = [function foo() {
    dosomething();
}];
```

选项 `{ "multiline": true, "minItems": 2 }`  的 **正确** 代码示例：

```js
/*eslint array-bracket-newline: ["error", { "multiline": true, "minItems": 2 }]*/

var a = [];
var b = [1];
var c = [
    1, 2
];
var d = [
    1,
    2
];
var e = [
    function foo() {
        dosomething();
    }
];
```

## 禁用建议

如果不希望对数组左括号后和右括号前强制换行，可以禁用此规则。

## 兼容

* **JSCS:** [validateNewlineAfterArrayElements](https://jscs-dev.github.io/rule/validateNewlineAfterArrayElements)
