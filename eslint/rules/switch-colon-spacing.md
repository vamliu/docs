---
规则名: switch-colon-spacing
规则类型: layout
---



Spacing around colons improves readability of `case`/`default` clauses.

## 规则详解

This rule controls spacing around colons of `case` and `default` clauses in `switch` statements.
This rule does the check only if the consecutive tokens exist on the same line.

This rule has 2 options that are boolean value.

```json
{
    "switch-colon-spacing": ["error", {"after": true, "before": false}]
}
```

* `"after": true` (Default) requires one or more spaces after colons.
* `"after": false` disallows spaces after colons.
* `"before": true` requires one or more spaces before colons.
* `"before": false` (Default) disallows before colons.

此规则的 **错误** 代码实例：



```js
/*eslint switch-colon-spacing: "error"*/

switch (a) {
    case 0 :break;
    default :foo();
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint switch-colon-spacing: "error"*/

switch (a) {
    case 0: foo(); break;
    case 1:
        bar();
        break;
    default:
        baz();
        break;
}
```

Examples of **incorrect** code for this rule with `{"after": false, "before": true}` option:



```js
/*eslint switch-colon-spacing: ["error", {"after": false, "before": true}]*/

switch (a) {
    case 0: break;
    default: foo();
}
```

Examples of **correct** code for this rule with `{"after": false, "before": true}` option:

::: correct

```js
/*eslint switch-colon-spacing: ["error", {"after": false, "before": true}]*/

switch (a) {
    case 0 :foo(); break;
    case 1 :
        bar();
        break;
    default :
        baz();
        break;
}
```

## 禁用建议

If you don't want to notify spacing around colons of switch statements, then it's safe to disable this rule.
