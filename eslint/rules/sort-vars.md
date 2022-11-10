---
规则名: sort-vars
规则类型: suggestion
关联规则:
- sort-keys
- sort-imports
---



When declaring multiple variables within the same block, some developers prefer to sort variable names alphabetically to be able to find necessary variable easier at the later time. Others feel that it adds complexity and becomes burden to maintain.

## 规则详解

This rule checks all variable declaration blocks and verifies that all variables are sorted alphabetically.
The default configuration of the rule is case-sensitive.

此规则的 **错误** 代码实例：



```js
/*eslint sort-vars: "error"*/

var b, a;

var a, B, c;

var a, A;
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint sort-vars: "error"*/

var a, b, c, d;

var _a = 10;
var _b = 20;

var A, a;

var B, a, c;
```

Alphabetical list is maintained starting from the first variable and excluding any that are considered problems. So the following code will produce two problems:

```js
/*eslint sort-vars: "error"*/

var c, d, a, b;
```

But this one, will only produce one:

```js
/*eslint sort-vars: "error"*/

var c, d, a, e;
```

## 配置项

This rule has an object option:

* `"ignoreCase": true` (default `false`) ignores the case-sensitivity of the variables order

### ignoreCase

选项 `{ "ignoreCase": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint sort-vars: ["error", { "ignoreCase": true }]*/

var a, A;

var a, B, c;
```

## 禁用建议

This rule is a formatting preference and not following it won't negatively affect the quality of your code. If you alphabetizing variables isn't a part of your coding standards, then you can leave this rule off.
