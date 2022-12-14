---
规则名: no-new-object
规则类型: suggestion
关联规则:
- no-array-constructor
- no-new-wrappers
---


The `Object` constructor is used to create new generic objects in JavaScript, such as:

```js
var myObject = new Object();
```

However, this is no different from using the more concise object literal syntax:

```js
var myObject = {};
```

For this reason, many prefer to always use the object literal syntax and never use the `Object` constructor.

While there are no performance differences between the two approaches, the byte savings and conciseness of the object literal form is what has made it the de facto way of creating new objects.

## 规则详解

This rule disallows `Object` constructors.

此规则的 **错误** 代码实例：



```js
/*eslint no-new-object: "error"*/

var myObject = new Object();

new Object();
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-new-object: "error"*/

var myObject = new CustomObject();

var myObject = {};

var Object = function Object() {};
new Object();
```

## 禁用建议

If you wish to allow the use of the `Object` constructor, you can safely turn this rule off.
