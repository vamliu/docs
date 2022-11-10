---
规则名: max-depth
规则类型: suggestion
关联规则:
- complexity
- max-len
- max-lines
- max-lines-per-function
- max-nested-callbacks
- max-params
- max-statements
---


Many developers consider code difficult to read if blocks are nested beyond a certain depth.

## 规则详解

This rule enforces a maximum depth that blocks can be nested to reduce code complexity.

## 配置项

This rule has a number or object option:

* `"max"` (default `4`) enforces a maximum depth that blocks can be nested

**Deprecated:** The object property `maximum` is deprecated; please use the object property `max` instead.

### max

选项 `{ "max": 4 }`  默认值的 **错误** 代码示例：



```js
/*eslint max-depth: ["error", 4]*/

function foo() {
    for (;;) { // Nested 1 deep
        while (true) { // Nested 2 deep
            if (true) { // Nested 3 deep
                if (true) { // Nested 4 deep
                    if (true) { // Nested 5 deep
                    }
                }
            }
        }
    }
}
```

选项 `{ "max": 4 }` 默认值的 **正确** 代码示例：

::: correct

```js
/*eslint max-depth: ["error", 4]*/

function foo() {
    for (;;) { // Nested 1 deep
        while (true) { // Nested 2 deep
            if (true) { // Nested 3 deep
                if (true) { // Nested 4 deep
                }
            }
        }
    }
}
```

Note that class static blocks do not count as nested blocks, and that the depth in them is calculated separately from the enclosing context.

Examples of **incorrect** code for this rule with `{ "max": 2 }` option:



```js
/*eslint max-depth: ["error", 2]*/

function foo() {
    if (true) { // Nested 1 deep
        class C {
            static {
                if (true) { // Nested 1 deep
                    if (true) { // Nested 2 deep
                        if (true) { // Nested 3 deep
                        }
                    }
                }
            }
        }
    }
}
```

Examples of **correct** code for this rule with `{ "max": 2 }` option:

::: correct

```js
/*eslint max-depth: ["error", 2]*/

function foo() {
    if (true) { // Nested 1 deep
        class C {
            static {
                if (true) { // Nested 1 deep
                    if (true) { // Nested 2 deep
                    }
                }
            }
        }
    }
}
```
