---
规则名: no-useless-escape
规则类型: suggestion
---





Escaping non-special characters in strings, template literals, and regular expressions doesn't have any effect, as demonstrated in the following example:

```js
let foo = "hol\a"; // > foo = "hola"
let bar = `${foo}\!`; // > bar = "hola!"
let baz = /\:/ // same functionality with /:/
```

## 规则详解

This rule flags escapes that can be safely removed without changing behavior.

此规则的 **错误** 代码实例：



```js
/*eslint no-useless-escape: "error"*/

"\'";
'\"';
"\#";
"\e";
`\"`;
`\"${foo}\"`;
`\#{foo}`;
/\!/;
/\@/;
/[\[]/;
/[a-z\-]/;
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-useless-escape: "error"*/

"\"";
'\'';
"\x12";
"\u00a9";
"\371";
"xs\u2111";
`\``;
`\${${foo}}`;
`$\{${foo}}`;
/\\/g;
/\t/g;
/\w\$\*\^\./;
/[[]/;
/[\]]/;
/[a-z-]/;
```

## 禁用建议

If you don't want to be notified about unnecessary escapes, you can safely disable this rule.
