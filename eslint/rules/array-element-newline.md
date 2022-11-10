---
规则名: array-element-newline
规则类型: layout
关联规则:
- array-bracket-spacing
- array-bracket-newline
- object-property-newline
- object-curly-spacing
- object-curly-newline
- max-statements-per-line
- block-spacing
- brace-style
---


许多样式规范都限制了是否使用数组内元素之间的换行符。

## 规则详解

此规则在数组内元素之间强制换行。

## 配置项

此规则有一个字符串选项：

* `"always"` （默认值）数组内元素之间需要换行
* `"never"` 禁用数组内元素之间的换行符
* `"consistent"` 需要在数组元素之间统一使用换行符

此外，还提供一个对象选项（如果满足任何属性，则需要换行。否则，不允许换行）：

* `"multiline": <boolean>` 如果元素中有换行符，则需要换行符。如果设为 `false` ，则禁用此条件。
* `"minItems": <number>` 如果元素数不少于给定整数，则需要换行。如果该值为 `0` ，则该条件的作用与选项 `"always"` 相同。如果此值为 `null` （默认值），则禁用此条件。

或者也可以为数组表达式和数组解构设置不同的配置：

```json
{
    "array-element-newline": ["error", {
        "ArrayExpression": "consistent",
        "ArrayPattern": { "minItems": 3 },
    }]
}
```

* `"ArrayExpression"` 数组表达式的配置（如果未指定，此规则不会对数组表达式生效）
* `"ArrayPattern"` 数组解构的配置（如果未指定，此规则不会对数组解构生效）

### always

选项 `"always"`  默认值的 **错误** 代码示例：

```js
/*eslint array-element-newline: ["error", "always"]*/

var c = [1, 2];
var d = [1, 2, 3];
var e = [1, 2, 3
];
var f = [
  1, 2, 3
];
var g = [
    function foo() {
        dosomething();
    }, function bar() {
        dosomething();
    }
];
```

选项 `"always"` 默认值的 **正确** 代码示例：

```js
/*eslint array-element-newline: ["error", "always"]*/

var a = [];
var b = [1];
var c = [1,
    2];
var d = [1,
    2,
    3];
var d = [
  1, 
  2, 
  3
];
var e = [
    function foo() {
        dosomething();
    },
    function bar() {
        dosomething();
    }
];
```

### never

选项 `"never"` 的 **错误** 代码示例：

```js
/*eslint array-element-newline: ["error", "never"]*/

var c = [
    1,
    2
];
var d = [
    1,
    2,
    3
];
var e = [
    function foo() {
        dosomething();
    },
    function bar() {
        dosomething();
    }
];
```

选项 `"never"` 的 **正确** 代码示例：

```js
/*eslint array-element-newline: ["error", "never"]*/

var a = [];
var b = [1];
var c = [1, 2];
var d = [1, 2, 3];
var e = [
    1, 2, 3];
var f = [
  1, 2, 3
];
var g = [
    function foo() {
        dosomething();
    }, function bar() {
        dosomething();
    }
];
```

### consistent

选项 `"consistent"` 的 **错误** 代码示例：

```js
/*eslint array-element-newline: ["error", "consistent"]*/

var a = [
    1, 2,
    3
];
var b = [
    function foo() {
        dosomething();
    }, function bar() {
        dosomething();
    },
    function baz() {
        dosomething();
    }
];
```

选项 `"consistent"` 的 **正确** 代码示例：

```js
/*eslint array-element-newline: ["error", "consistent"]*/

var a = [];
var b = [1];
var c = [1, 2];
var d = [1, 2, 3];
var e = [
    1,
    2
];
var f = [
    1,
    2,
    3
];
var g = [
    function foo() {
        dosomething();
    }, function bar() {
        dosomething();
    }, function baz() {
        dosomething();
    }
];
var h = [
    function foo() {
        dosomething();
    },
    function bar() {
        dosomething();
    },
    function baz() {
        dosomething();
    }
];
```

### multiline

选项 `{ "multiline": true }` 的 **错误** 代码示例：

```js
/*eslint array-element-newline: ["error", { "multiline": true }]*/

var d = [1,
    2, 3];
var e = [
    function foo() {
        dosomething();
    }, function bar() {
        dosomething();
    }
];
```

选项 `{ "multiline": true }` 的 **正确** 代码示例：

```js
/*eslint array-element-newline: ["error", { "multiline": true }]*/

var a = [];
var b = [1];
var c = [1, 2];
var d = [1, 2, 3];
var e = [
    function foo() {
        dosomething();
    },
    function bar() {
        dosomething();
    }
];
```

### minItems

选项 `{ "minItems": 3 }` 的 **错误** 代码示例：

```js
/*eslint array-element-newline: ["error", { "minItems": 3 }]*/

var c = [1,
    2];
var d = [1, 2, 3];
var e = [
    function foo() {
        dosomething();
    },
    function bar() {
        dosomething();
    }
];
```

选项 `{ "minItems": 3 }` 的 **正确** 代码示例：

```js
/*eslint array-element-newline: ["error", { "minItems": 3 }]*/

var a = [];
var b = [1];
var c = [1, 2];
var d = [1,
    2,
    3];
var e = [
    function foo() {
        dosomething();
    }, function bar() {
        dosomething();
    }
];
```

### multiline and minItems

选项 `{ "multiline": true, "minItems": 3 }`  的 **错误** 代码示例：

```js
/*eslint array-element-newline: ["error", { "multiline": true, "minItems": 3 }]*/

var c = [1,
2];
var d = [1, 2, 3];
var e = [
    function foo() {
        dosomething();
    }, function bar() {
        dosomething();
    }
];
```

选项 `{ "multiline": true, "minItems": 3 }`  的 **正确** 代码示例：

```js
/*eslint array-element-newline: ["error", { "multiline": true, "minItems": 3 }]*/

var a = [];
var b = [1];
var c = [1, 2];
var d = [1,
    2,
    3];
var e = [
    function foo() {
        dosomething();
    },
    function bar() {
        dosomething();
    }
];
```

### ArrayExpression and ArrayPattern

选项 `{ "ArrayExpression": "always", "ArrayPattern": "never" }`  的 **错误** 代码示例：

```js
/*eslint array-element-newline: ["error", { "ArrayExpression": "always", "ArrayPattern": "never" }]*/

var a = [1, 2];
var b = [1, 2, 3];
var c = [
    function foo() {
        dosomething();
    }, function bar() {
        dosomething();
    }
];

var [d,
    e] = arr;
var [f,
    g,
    h] = arr;
var [i = function foo() {
  dosomething()
},
j = function bar() {
  dosomething()
}] = arr
```

选项 `{ "ArrayExpression": "always", "ArrayPattern": "never" }`  的 **正确** 代码示例：

```js
/*eslint array-element-newline: ["error", { "ArrayExpression": "always", "ArrayPattern": "never" }]*/

var a = [1,
    2];
var b = [1,
    2,
    3];
var c = [
    function foo() {
        dosomething();
    },
    function bar() {
        dosomething();
    }
];

var [d, e] = arr
var [f, g, h] = arr
var [i = function foo() {
    dosomething()
}, j = function bar() {
    dosomething()
}] = arr
```

## 禁用建议

如果你不想让数组内元素强制换行，可以不启用此规则。

## 兼容

* **JSCS:** [validateNewlineAfterArrayElements](https://jscs-dev.github.io/rule/validateNewlineAfterArrayElements)
