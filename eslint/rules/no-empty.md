---
规则名: no-empty
规则类型: suggestion
关联规则:
- no-empty-function
---



Empty block statements, while not technically errors, usually occur due to refactoring that wasn't completed. They can cause confusion when reading code.

## 规则详解

This rule disallows empty block statements. This rule ignores block statements which contain a comment (for example, in an empty `catch` or `finally` block of a `try` statement to indicate that execution should continue regardless of errors).

此规则的 **错误** 代码实例：



```js
/*eslint no-empty: "error"*/

if (foo) {
}

while (foo) {
}

switch(foo) {
}

try {
    doSomething();
} catch(ex) {

} finally {

}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-empty: "error"*/

if (foo) {
    // empty
}

while (foo) {
    /* empty */
}

try {
    doSomething();
} catch (ex) {
    // continue regardless of error
}

try {
    doSomething();
} finally {
    /* continue regardless of error */
}
```

## 配置项

This rule has an object option for exceptions:

* `"allowEmptyCatch": true` allows empty `catch` clauses (that is, which do not contain a comment)

### allowEmptyCatch

Examples of additional **correct** code for this rule with the `{ "allowEmptyCatch": true }` option:

::: correct

```js
/* eslint no-empty: ["error", { "allowEmptyCatch": true }] */
try {
    doSomething();
} catch (ex) {}

try {
    doSomething();
}
catch (ex) {}
finally {
    /* continue regardless of error */
}
```

## 禁用建议

If you intentionally use empty block statements then you can disable this rule.
