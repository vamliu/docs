---
规则名: no-empty-static-block
规则类型: suggestion
关联规则:
- no-empty
- no-empty-function
深入了解:
- https://github.com/tc39/proposal-class-static-block
---

Empty static blocks, while not technically errors, usually occur due to refactoring that wasn't completed. They can cause confusion when reading code.

## 规则详解

This rule disallows empty static blocks. This rule ignores static blocks which contain a comment.

此规则的 **错误** 代码实例：



```js
/*eslint no-empty-static-block: "error"*/

class Foo {
    static {}
}
```

此规则的 **正确** 代码实例：

```js
/*eslint no-empty-static-block: "error"*/

class Foo {
    static {
        bar();
    }
}

class Foo {
    static {
        // comment
    }
}
```

## 禁用建议

This rule should not be used in environments prior to ES2022.
