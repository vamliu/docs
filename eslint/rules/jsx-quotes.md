---
规则名: jsx-quotes
规则类型: layout
关联规则:
- quotes
---



JSX attribute values can contain string literals, which are delimited with single or double quotes.

```xml
<a b='c' />
<a b="c" />
```

Unlike string literals in JavaScript, string literals within JSX attributes can’t contain escaped quotes.
If you want to have e.g. a double quote within a JSX attribute value, you have to use single quotes as string delimiter.

```xml
<a b="'" />
<a b='"' />
```

## 规则详解

This rule enforces the consistent use of either double or single quotes in JSX attributes.

## 配置项

This rule has a string option:

* `"prefer-double"` (default) enforces the use of double quotes for all JSX attribute values that don't contain a double quote.
* `"prefer-single"` enforces the use of single quotes for all JSX attribute values that don’t contain a single quote.

### prefer-double

选项 `"prefer-double"`  默认值的 **错误** 代码示例：

```xml
/*eslint jsx-quotes: ["error", "prefer-double"]*/

<a b='c' />
```

选项 `"prefer-double"` 默认值的 **正确** 代码示例：

```xml
/*eslint jsx-quotes: ["error", "prefer-double"]*/

<a b="c" />
<a b='"' />
```

### prefer-single

选项 `"prefer-single"` 的 **错误** 代码示例：

```xml
/*eslint jsx-quotes: ["error", "prefer-single"]*/

<a b="c" />
```

选项 `"prefer-single"` 的 **正确** 代码示例：

```xml
/*eslint jsx-quotes: ["error", "prefer-single"]*/

<a b='c' />
<a b="'" />
```

## 禁用建议

You can turn this rule off if you don’t use JSX or if you aren’t concerned with a consistent usage of quotes within JSX attributes.
