---
规则名: no-this-before-super
规则类型: problem
---



In the constructor of derived classes, if `this`/`super` are used before `super()` calls, it raises a reference error.

This rule checks `this`/`super` keywords in constructors, then reports those that are before `super()`.

## 规则详解

This rule is aimed to flag `this`/`super` keywords before `super()` callings.

## Examples

此规则的 **错误** 代码实例：



```js
/*eslint no-this-before-super: "error"*/
/*eslint-env es6*/

class A extends B {
    constructor() {
        this.a = 0;
        super();
    }
}

class A extends B {
    constructor() {
        this.foo();
        super();
    }
}

class A extends B {
    constructor() {
        super.foo();
        super();
    }
}

class A extends B {
    constructor() {
        super(this.foo());
    }
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-this-before-super: "error"*/
/*eslint-env es6*/

class A {
    constructor() {
        this.a = 0; // OK, this class doesn't have an `extends` clause.
    }
}

class A extends B {
    constructor() {
        super();
        this.a = 0; // OK, this is after `super()`.
    }
}

class A extends B {
    foo() {
        this.a = 0; // OK. this is not in a constructor.
    }
}
```

## 禁用建议

If you don't want to be notified about using `this`/`super` before `super()` in constructors, you can safely disable this rule.
