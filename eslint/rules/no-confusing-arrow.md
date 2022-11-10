---
规则名: no-confusing-arrow
规则类型: suggestion
关联规则:
- no-constant-condition
- arrow-parens
---



Arrow functions (`=>`) are similar in syntax to some comparison operators (`>`, `<`, `<=`, and `>=`). This rule warns against using the arrow function syntax in places where it could be confused with a comparison operator.

Here's an example where the usage of `=>` could be confusing:

```js
// The intent is not clear
var x = a => 1 ? 2 : 3;
// Did the author mean this
var x = function (a) {
    return 1 ? 2 : 3;
};
// Or this
var x = a <= 1 ? 2 : 3;
```

## 规则详解

此规则的 **错误** 代码实例：



```js
/*eslint no-confusing-arrow: "error"*/
/*eslint-env es6*/

var x = a => 1 ? 2 : 3;
var x = (a) => 1 ? 2 : 3;
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-confusing-arrow: "error"*/
/*eslint-env es6*/
var x = a => (1 ? 2 : 3);
var x = (a) => (1 ? 2 : 3);
var x = (a) => {
    return 1 ? 2 : 3;
};
var x = a => { return 1 ? 2 : 3; };
```

## 配置项

This rule accepts two options argument with the following defaults:

```json
{
    "rules": {
        "no-confusing-arrow": [
            "error",
            { "allowParens": true, "onlyOneSimpleParam": false }
        ]
    }
}
```

`allowParens` is a boolean setting that can be `true`(default) or `false`:

1. `true` relaxes the rule and accepts parenthesis as a valid "confusion-preventing" syntax.
2. `false` warns even if the expression is wrapped in parenthesis

选项 `{"allowParens": false}` 的 **错误** 代码示例：



```js
/*eslint no-confusing-arrow: ["error", {"allowParens": false}]*/
/*eslint-env es6*/
var x = a => (1 ? 2 : 3);
var x = (a) => (1 ? 2 : 3);
```

`onlyOneSimpleParam` is a boolean setting that can be `true` or `false`(default):

1. `true` relaxes the rule and doesn't report errors if the arrow function has 0 or more than 1 parameters, or the parameter is not an identifier.
2. `false` warns regardless of parameters.

选项 `{"onlyOneSimpleParam": true}` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-confusing-arrow: ["error", {"onlyOneSimpleParam": true}]*/
/*eslint-env es6*/
() => 1 ? 2 : 3;
(a, b) => 1 ? 2 : 3;
(a = b) => 1 ? 2 : 3;
({ a }) => 1 ? 2 : 3;
([a]) => 1 ? 2 : 3;
(...a) => 1 ? 2 : 3;
```
