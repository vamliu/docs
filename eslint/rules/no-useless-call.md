---
规则名: no-useless-call
规则类型: suggestion
关联规则:
- prefer-spread
---


The function invocation can be written by `Function.prototype.call()` and `Function.prototype.apply()`.
But `Function.prototype.call()` and `Function.prototype.apply()` are slower than the normal function invocation.

## 规则详解

This rule is aimed to flag usage of `Function.prototype.call()` and `Function.prototype.apply()` that can be replaced with the normal function invocation.

此规则的 **错误** 代码实例：



```js
/*eslint no-useless-call: "error"*/

// These are same as `foo(1, 2, 3);`
foo.call(undefined, 1, 2, 3);
foo.apply(undefined, [1, 2, 3]);
foo.call(null, 1, 2, 3);
foo.apply(null, [1, 2, 3]);

// These are same as `obj.foo(1, 2, 3);`
obj.foo.call(obj, 1, 2, 3);
obj.foo.apply(obj, [1, 2, 3]);
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-useless-call: "error"*/

// The `this` binding is different.
foo.call(obj, 1, 2, 3);
foo.apply(obj, [1, 2, 3]);
obj.foo.call(null, 1, 2, 3);
obj.foo.apply(null, [1, 2, 3]);
obj.foo.call(otherObj, 1, 2, 3);
obj.foo.apply(otherObj, [1, 2, 3]);

// The argument list is variadic.
// Those are warned by the `prefer-spread` rule.
foo.apply(undefined, args);
foo.apply(null, args);
obj.foo.apply(obj, args);
```

## 已知局限

This rule compares code statically to check whether or not `thisArg` is changed.
So if the code about `thisArg` is a dynamic expression, this rule cannot judge correctly.

此规则的 **错误** 代码实例：



```js
/*eslint no-useless-call: "error"*/

a[i++].foo.call(a[i++], 1, 2, 3);
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-useless-call: "error"*/

a[++i].foo.call(a[i], 1, 2, 3);
```

## 禁用建议

If you don't want to be notified about unnecessary `.call()` and `.apply()`, you can safely disable this rule.
