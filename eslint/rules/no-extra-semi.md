---
规则名: no-extra-semi
规则类型: suggestion
关联规则:
- semi
- semi-spacing
---





Typing mistakes and misunderstandings about where semicolons are required can lead to semicolons that are unnecessary. While not technically an error, extra semicolons can cause confusion when reading code.

## 规则详解

This rule disallows unnecessary semicolons.

此规则的 **错误** 代码实例：



```js
/*eslint no-extra-semi: "error"*/

var x = 5;;

function foo() {
    // code
};

class C {
    field;;

    method() {
        // code
    };

    static {
        // code
    };
};
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-extra-semi: "error"*/

var x = 5;

function foo() {
    // code
}

var bar = function() {
    // code
};

class C {
    field;

    method() {
        // code
    }

    static {
        // code
    }
}
```

## 禁用建议

If you intentionally use extra semicolons then you can disable this rule.
