---
规则名: no-array-constructor
规则类型: suggestion
关联规则:
- no-new-object
- no-new-wrappers
---


Use of the `Array` constructor to construct a new array is generally
discouraged in favor of array literal notation because of the single-argument
pitfall and because the `Array` global may be redefined. The exception is when
the Array constructor is used to intentionally create sparse arrays of a
specified size by giving the constructor a single numeric argument.

## 规则详解

This rule disallows `Array` constructors.

此规则的 **错误** 代码实例：

```js
/*eslint no-array-constructor: "error"*/

Array(0, 1, 2)

new Array(0, 1, 2)
```

此规则的 **正确** 代码实例：

```js
/*eslint no-array-constructor: "error"*/

Array(500)

new Array(someOtherArray.length)

[0, 1, 2]
```

## 禁用建议

This rule enforces a nearly universal stylistic concern. That being said, this
rule may be disabled if the constructor style is preferred.
