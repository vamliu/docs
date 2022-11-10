---
规则名: logical-assignment-operators
规则类型: suggestion
---

ES2021 introduces the assignment operator shorthand for the logical operators `||`, `&&` and `??`.
Before, this was only allowed for mathematical operations such as `+` or `*` (see the rule [operator-assignment](./operator-assignment)).
The shorthand can be used if the assignment target and the left expression of a logical expression are the same.
For example `a = a || b` can be shortened to `a ||= b`.

## 规则详解

This rule requires or disallows logical assignment operator shorthand.  

### 配置项

This rule has a string and an object option.
String option:

* `"always"` (default)
* `"never"`

Object option (only available if string option is set to `"always"`):

* `"enforceForIfStatements": false`(default) Do *not* check for equivalent `if` statements
* `"enforceForIfStatements": true` Check for equivalent `if` statements

#### always

选项 `"always"`  默认值的 **错误** 代码示例：



```js
/*eslint logical-assignment-operators: ["error", "always"]*/

a = a || b
a = a && b
a = a ?? b
a || (a = b)
a && (a = b)
a ?? (a = b)
```

选项 `"always"` 默认值的 **正确** 代码示例：

::: correct

```js
/*eslint logical-assignment-operators: ["error", "always"]*/

a = b
a += b
a ||= b
a = b || c
a || (b = c)

if (a) a = b
```

#### never

选项 `"never"` 的 **错误** 代码示例：



```js
/*eslint logical-assignment-operators: ["error", "never"]*/

a ||= b
a &&= b
a ??= b
```

选项 `"never"` 的 **正确** 代码示例：

::: correct

```js
/*eslint logical-assignment-operators: ["error", "never"]*/

a = a || b
a = a && b
a = a ?? b
```

#### enforceForIfStatements

This option checks for additional patterns with if statements which could be expressed with the logical assignment operator.



选项 `["always", { enforceForIfStatements: true }]` 的 **错误** 代码示例：

```js
/*eslint logical-assignment-operators: ["error", "always", { enforceForIfStatements: true }]*/

if (a) a = b // <=> a &&= b
if (!a) a = b // <=> a ||= b

if (a == null) a = b // <=> a ??= b
if (a === null || a === undefined) a = b // <=> a ??= b
```

选项 `["always", { enforceForIfStatements: true }]` 的 **正确** 代码示例：

::: correct

```js
/*eslint logical-assignment-operators: ["error", "always", { enforceForIfStatements: true }]*/

if (a) b = c
if (a === 0) a = b
```

## 禁用建议

Use of logical operator assignment shorthand is a stylistic choice. Leaving this rule turned off would allow developers to choose which style is more readable on a case-by-case basis.
