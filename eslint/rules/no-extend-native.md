---
规则名: no-extend-native
布局: doc
规则类型: suggestion
关联规则:
- no-global-assign
---


In JavaScript, you can extend any object, including builtin or "native" objects. Sometimes people change the behavior of these native objects in ways that break the assumptions made about them in other parts of the code.

For example here we are overriding a builtin method that will then affect all Objects, even other builtins.

```js
// seems harmless
Object.prototype.extra = 55;

// loop through some userIds
var users = {
    "123": "Stan",
    "456": "David"
};

// not what you'd expect
for (var id in users) {
    console.log(id); // "123", "456", "extra"
}
```

A common suggestion to avoid this problem would be to wrap the inside of the `for` loop with `users.hasOwnProperty(id)`. However, if this rule is strictly enforced throughout your codebase you won't need to take that step.

## 规则详解

Disallows directly modifying the prototype of builtin objects.

Examples of **incorrect** code for this rule:



```js
/*eslint no-extend-native: "error"*/

Object.prototype.a = "a";
Object.defineProperty(Array.prototype, "times", { value: 999 });
```

## 配置项

This rule accepts an `exceptions` option, which can be used to specify a list of builtins for which extensions will be allowed.

### exceptions

选项 sample `{ "exceptions": ["Object"] }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-extend-native: ["error", { "exceptions": ["Object"] }]*/

Object.prototype.a = "a";
```

## 已知局限

This rule *does not* report any of the following less obvious approaches to modify the prototype of builtin objects:

```js
var x = Object;
x.prototype.thing = a;

eval("Array.prototype.forEach = 'muhahaha'");

with(Array) {
    prototype.thing = 'thing';
};

window.Function.prototype.bind = 'tight';
```

## 使用建议

You may want to disable this rule when working with polyfills that try to patch older versions of JavaScript with the latest spec, such as those that might `Function.prototype.bind` or `Array.prototype.forEach` in a future-friendly way.
