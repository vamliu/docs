---
规则名: constructor-super
规则类型: problem
---

Constructors of derived classes must call `super()`.
Constructors of non derived classes must not call `super()`.
If this is not observed, the JavaScript engine will raise a runtime error.

This rule checks whether or not there is a valid `super()` call.

## 规则详解

This rule is aimed to flag invalid/missing `super()` calls.

此规则的 **错误** 代码实例：

```js
/*eslint constructor-super: "error"*/
/*eslint-env es6*/

class A {
    constructor() {
        super();  // This is a SyntaxError.
    }
}

class A extends B {
    constructor() { }  // Would throw a ReferenceError.
}

// Classes which inherits from a non constructor are always problems.
class A extends null {
    constructor() {
        super();  // Would throw a TypeError.
    }
}

class A extends null {
    constructor() { }  // Would throw a ReferenceError.
}
```

此规则的 **正确** 代码实例：

```js
/*eslint constructor-super: "error"*/
/*eslint-env es6*/

class A {
    constructor() { }
}

class A extends B {
    constructor() {
        super();
    }
}
```

## 禁用建议

If you don't want to be notified about invalid/missing `super()` callings in constructors, you can safely disable this rule.
