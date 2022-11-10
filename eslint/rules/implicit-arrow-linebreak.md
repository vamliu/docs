---
规则名: implicit-arrow-linebreak
规则类型: layout
关联规则:
- brace-style
---



An arrow function body can contain an implicit return as an expression instead of a block body. It can be useful to enforce a consistent location for the implicitly returned expression.

## 规则详解

This rule aims to enforce a consistent location for an arrow function containing an implicit return.

### 配置项

This rule accepts a string option:

* `"beside"` (default) disallows a newline before an arrow function body.
* `"below"` requires a newline before an arrow function body.

选项 `"beside"`  默认值的 **错误** 代码示例：



```js
/* eslint implicit-arrow-linebreak: ["error", "beside"] */

(foo) =>
  bar;

(foo) =>
  (bar);

(foo) =>
  bar =>
    baz;

(foo) =>
(
  bar()
);
```

选项 `"beside"` 默认值的 **正确** 代码示例：

::: correct

```js
/* eslint implicit-arrow-linebreak: ["error", "beside"] */

(foo) => bar;

(foo) => (bar);

(foo) => bar => baz;

(foo) => (
  bar()
);

// functions with block bodies allowed with this rule using any style
// to enforce a consistent location for this case, see the rule: `brace-style`
(foo) => {
  return bar();
}

(foo) =>
{
  return bar();
}
```

选项 `"below"` 的 **错误** 代码示例：



```js
/* eslint implicit-arrow-linebreak: ["error", "below"] */

(foo) => bar;

(foo) => (bar);

(foo) => bar => baz;
```

选项 `"below"` 的 **正确** 代码示例：

::: correct

```js
/* eslint implicit-arrow-linebreak: ["error", "below"] */

(foo) =>
  bar;

(foo) =>
  (bar);

(foo) =>
  bar =>
    baz;
```

## 禁用建议

If you're not concerned about consistent locations of implicitly returned arrow function expressions, you should not turn on this rule.

You can also disable this rule if you are using the `"always"` option for the [`arrow-body-style`](arrow-body-style), since this will disable the use of implicit returns in arrow functions.
