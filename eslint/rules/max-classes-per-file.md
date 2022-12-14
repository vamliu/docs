---
规则名: max-classes-per-file
规则类型: suggestion
---


Files containing multiple classes can often result in a less navigable
and poorly structured codebase. Best practice is to keep each file
limited to a single responsibility.

## 规则详解

This rule enforces that each file may contain only a particular number
of classes and no more.

此规则的 **错误** 代码实例：



```js
/*eslint max-classes-per-file: "error"*/

class Foo {}
class Bar {}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint max-classes-per-file: "error"*/

class Foo {}
```

## 配置项

This rule may be configured with either an object or a number.

If the option is an object, it may contain one or both of:

* `ignoreExpressions`: a boolean option (defaulted to `false`) to ignore class expressions.
* `max`: a numeric option (defaulted to 1) to specify the maximum number of classes.

For example:

```json
{
    "max-classes-per-file": ["error", 1]
}
```

```json
{
    "max-classes-per-file": [
        "error",
        { "ignoreExpressions": true, "max": 2 }
    ]
}
```

Examples of **correct** code for this rule with the `max` option set to `2`:

::: correct

```js
/* eslint max-classes-per-file: ["error", 2] */

class Foo {}
class Bar {}
```

Examples of **correct** code for this rule with the `ignoreExpressions` option set to `true`:

::: correct

```js
/* eslint max-classes-per-file: ["error", { ignoreExpressions: true }] */

class VisitorFactory {
    forDescriptor(descriptor) {
        return class {
            visit(node) {
                return `Visiting ${descriptor}.`;
            }
        };
    }
}
```
