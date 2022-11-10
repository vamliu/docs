---
规则名: no-useless-constructor
规则类型: suggestion
---


ES2015 provides a default class constructor if one is not specified. As such, it is unnecessary to provide an empty constructor or one that simply delegates into its parent class, as in the following examples:

```js
class A {
    constructor () {
    }
}

class B extends A {
    constructor (value) {
      super(value);
    }
}
```

## 规则详解

This rule flags class constructors that can be safely removed without changing how the class works.

## Examples

此规则的 **错误** 代码实例：



```js
/*eslint no-useless-constructor: "error"*/
/*eslint-env es6*/

class A {
    constructor () {
    }
}

class B extends A {
    constructor (...args) {
      super(...args);
    }
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-useless-constructor: "error"*/

class A { }

class A {
    constructor () {
        doSomething();
    }
}

class B extends A {
    constructor() {
        super('foo');
    }
}

class B extends A {
    constructor() {
        super();
        doSomething();
    }
}
```

## 禁用建议

If you don't want to be notified about unnecessary constructors, you can safely disable this rule.
