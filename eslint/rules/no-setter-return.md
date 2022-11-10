---
规则名: no-setter-return
规则类型: problem
关联规则:
- getter-return
深入了解:
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/set
---



Setters cannot return values.

While returning a value from a setter does not produce an error, the returned value is being ignored. Therefore, returning a value from a setter is either unnecessary or a possible error, since the returned value cannot be used.

## 规则详解

This rule disallows returning values from setters and reports `return` statements in setter functions.

Only `return` without a value is allowed, as it's a control flow statement.

This rule checks setters in:

* Object literals.
* Class declarations and class expressions.
* Property descriptors in `Object.create`, `Object.defineProperty`, `Object.defineProperties`, and `Reflect.defineProperty` methods of the global objects.

此规则的 **错误** 代码实例：



```js
/*eslint no-setter-return: "error"*/

var foo = {
    set a(value) {
        this.val = value;
        return value;
    }
};

class Foo {
    set a(value) {
        this.val = value * 2;
        return this.val;
    }
}

const Bar = class {
    static set a(value) {
        if (value < 0) {
            this.val = 0;
            return 0;
        }
        this.val = value;
    }
};

Object.defineProperty(foo, "bar", {
    set(value) {
        if (value < 0) {
            return false;
        }
        this.val = value;
    }
});
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-setter-return: "error"*/

var foo = {
    set a(value) {
        this.val = value;
    }
};

class Foo {
    set a(value) {
        this.val = value * 2;
    }
}

const Bar = class {
    static set a(value) {
        if (value < 0) {
            this.val = 0;
            return;
        }
        this.val = value;
    }
};

Object.defineProperty(foo, "bar", {
    set(value) {
        if (value < 0) {
            throw new Error("Negative value.");
        }
        this.val = value;
    }
});
```
