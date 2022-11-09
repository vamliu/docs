---
规则名: dot-location
布局: doc
规则类型: layout
关联规则:
- newline-after-var
- dot-notation
---



JavaScript allows you to place newlines before or after a dot in a member expression.

Consistency in placing a newline before or after the dot can greatly increase readability.

```js
var a = universe.
        galaxy;

var b = universe
       .galaxy;
```

## 规则详解

This rule aims to enforce newline consistency in member expressions. This rule prevents the use of mixed newlines around the dot in a member expression.

## 配置项

The rule takes one option, a string:

* If it is `"object"` (default), the dot in a member expression should be on the same line as the object portion.
* If it is `"property"`, the dot in a member expression should be on the same line as the property portion.

### object

The default `"object"` option requires the dot to be on the same line as the object.

选项 default `"object"` 的 **错误** 代码示例：



```js
/*eslint dot-location: ["error", "object"]*/

var foo = object
.property;
```

选项 default `"object"` 的 **正确** 代码示例：

::: correct

```js
/*eslint dot-location: ["error", "object"]*/

var foo = object.
property;

var bar = (
    object
).
property;

var baz = object.property;
```

### property

The `"property"` option requires the dot to be on the same line as the property.

选项 `"property"` 的 **错误** 代码示例：



```js
/*eslint dot-location: ["error", "property"]*/

var foo = object.
property;
```

选项 `"property"` 的 **正确** 代码示例：

::: correct

```js
/*eslint dot-location: ["error", "property"]*/

var foo = object
.property;
var bar = object.property;
```

## 使用建议

You can turn this rule off if you are not concerned with the consistency of newlines before or after dots in member expressions.
