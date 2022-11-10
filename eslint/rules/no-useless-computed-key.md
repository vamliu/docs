---
规则名: no-useless-computed-key
规则类型: suggestion
---



It's unnecessary to use computed properties with literals such as:

```js
var foo = {["a"]: "b"};
```

The code can be rewritten as:

```js
var foo = {"a": "b"};
```

## 规则详解

This rule disallows unnecessary usage of computed property keys.

此规则的 **错误** 代码实例：



```js
/*eslint no-useless-computed-key: "error"*/

var a = { ['0']: 0 };
var a = { ['0+1,234']: 0 };
var a = { [0]: 0 };
var a = { ['x']: 0 };
var a = { ['x']() {} };
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-useless-computed-key: "error"*/

var c = { 'a': 0 };
var c = { 0: 0 };
var a = { x() {} };
var c = { a: 0 };
var c = { '0+1,234': 0 };
```

Examples of additional **correct** code for this rule:

::: correct

```js
/*eslint no-useless-computed-key: "error"*/

var c = {
    "__proto__": foo, // defines object's prototype

    ["__proto__"]: bar // defines a property named "__proto__"
};
```

## 配置项

This rule has an object option:

* `enforceForClassMembers` set to `true` additionally applies this rule to class members (Default `false`).

### enforceForClassMembers

By default, this rule does not check class declarations and class expressions,
as the default value for `enforceForClassMembers` is `false`.

When `enforceForClassMembers` is set to `true`, the rule will also disallow unnecessary computed keys inside of class fields, class methods, class getters, and class setters.

选项 `{ "enforceForClassMembers": true }` 的 **错误** 代码示例：



```js
/*eslint no-useless-computed-key: ["error", { "enforceForClassMembers": true }]*/

class Foo {
    ["foo"] = "bar";

    [0]() {}
    ['a']() {}
    get ['b']() {}
    set ['c'](value) {}

    static ["foo"] = "bar";

    static ['a']() {}
}
```

选项 `{ "enforceForClassMembers": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-useless-computed-key: ["error", { "enforceForClassMembers": true }]*/

class Foo {
    "foo" = "bar";

    0() {}
    'a'() {}
    get 'b'() {}
    set 'c'(value) {}

    static "foo" = "bar";

    static 'a'() {}
}
```

Examples of additional **correct** code for this rule with the `{ "enforceForClassMembers": true }` option:

::: correct

```js
/*eslint no-useless-computed-key: ["error", { "enforceForClassMembers": true }]*/

class Foo {
    ["constructor"]; // instance field named "constructor"

    "constructor"() {} // the constructor of this class

    ["constructor"]() {} // method named "constructor"

    static ["constructor"]; // static field named "constructor"

    static ["prototype"]; // runtime error, it would be a parsing error without `[]`
}
```

## 禁用建议

If you don't want to be notified about unnecessary computed property keys, you can safely disable this rule.
