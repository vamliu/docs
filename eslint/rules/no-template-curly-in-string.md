---
规则名: no-template-curly-in-string
规则类型: problem
---


ECMAScript 6 allows programmers to create strings containing variable or expressions using template literals, instead of string concatenation, by writing expressions like `${variable}` between two backtick quotes (\`). It can be easy to use the wrong quotes when wanting to use template literals, by writing `"${variable}"`, and end up with the literal value `"${variable}"` instead of a string containing the value of the injected expressions.

## 规则详解

This rule aims to warn when a regular string contains what looks like a template literal placeholder. It will warn when it finds a string containing the template literal placeholder (`${something}`) that uses either `"` or `'` for the quotes.

## Examples

此规则的 **错误** 代码实例：



```js
/*eslint no-template-curly-in-string: "error"*/
"Hello ${name}!";
'Hello ${name}!';
"Time: ${12 * 60 * 60 * 1000}";
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-template-curly-in-string: "error"*/
`Hello ${name}!`;
`Time: ${12 * 60 * 60 * 1000}`;

templateFunction`Hello ${name}`;
```

## 禁用建议

This rule should not be used in ES3/5 environments.
