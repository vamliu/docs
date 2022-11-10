---
规则名: template-tag-spacing
规则类型: layout
深入了解:
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#Tagged_template_literals
- https://exploringjs.com/es6/ch_template-literals.html#_examples-of-using-tagged-template-literals
---



With ES6, it's possible to create functions called [tagged template literals](#further-reading) where the function parameters consist of a template literal's strings and expressions.

When using tagged template literals, it's possible to insert whitespace between the tag function and the template literal. Since this whitespace is optional, the following lines are equivalent:

```js
let hello = func`Hello world`;
let hello = func `Hello world`;
```

## 规则详解

This rule aims to maintain consistency around the spacing between template tag functions and their template literals.

## 配置项

```json
{
    "template-tag-spacing": ["error", "never"]
}
```

This rule has one option whose value can be set to `"never"` or `"always"`

* `"never"` (default) - Disallows spaces between a tag function and its template literal.
* `"always"` - Requires one or more spaces between a tag function and its template literal.

## Examples

### never

选项 `"never"`  默认值的 **错误** 代码示例：



```js
/*eslint template-tag-spacing: "error"*/

func `Hello world`;
```

选项 `"never"` 默认值的 **正确** 代码示例：

::: correct

```js
/*eslint template-tag-spacing: "error"*/

func`Hello world`;
```

### always

选项 `"always"` 的 **错误** 代码示例：



```js
/*eslint template-tag-spacing: ["error", "always"]*/

func`Hello world`;
```

选项 `"always"` 的 **正确** 代码示例：

::: correct

```js
/*eslint template-tag-spacing: ["error", "always"]*/

func `Hello world`;
```

## 禁用建议

If you don't want to be notified about usage of spacing between tag functions and their template literals, then it's safe to disable this rule.
