---
规则名: template-curly-spacing
规则类型: layout
---



We can embed expressions in template strings with using a pair of `${` and `}`.

This rule can force usage of spacing _within_ the curly brace pair according to style guides.

```js
let hello = `hello, ${people.name}!`;
```

## 规则详解

This rule aims to maintain consistency around the spacing inside of template literals.

## 配置项

```json
{
    "template-curly-spacing": ["error", "never"]
}
```

This rule has one option which has either `"never"` or `"always"` as value.

* `"never"` (by default) - Disallows spaces inside of the curly brace pair.
* `"always"` - Requires one or more spaces inside of the curly brace pair.

## Examples

### never

选项 `"never"`  默认值的 **错误** 代码示例：



```js
/*eslint template-curly-spacing: "error"*/

`hello, ${ people.name}!`;
`hello, ${people.name }!`;

`hello, ${ people.name }!`;
```

选项 `"never"` 默认值的 **正确** 代码示例：

::: correct

```js
/*eslint template-curly-spacing: "error"*/

`hello, ${people.name}!`;

`hello, ${
    people.name
}!`;
```

### always

选项 `"always"` 的 **错误** 代码示例：



```js
/*eslint template-curly-spacing: ["error", "always"]*/

`hello, ${ people.name}!`;
`hello, ${people.name }!`;

`hello, ${people.name}!`;
```

选项 `"always"` 的 **正确** 代码示例：

::: correct

```js
/*eslint template-curly-spacing: ["error", "always"]*/

`hello, ${ people.name }!`;

`hello, ${
    people.name
}!`;
```

## 禁用建议

If you don't want to be notified about usage of spacing inside of template strings, then it's safe to disable this rule.
