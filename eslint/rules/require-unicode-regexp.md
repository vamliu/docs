---
规则名: require-unicode-regexp
规则类型: suggestion
---


RegExp `u` flag has two effects:

1. **Make the regular expression handling UTF-16 surrogate pairs correctly.**

    Especially, character range syntax gets the correct behavior.

    ```js
    /^[👍]$/.test("👍") //→ false
    /^[👍]$/u.test("👍") //→ true
    ```

2. **Make the regular expression throwing syntax errors early as disabling [Annex B extensions](https://www.ecma-international.org/ecma-262/6.0/#sec-regular-expressions-patterns).**

    Because of historical reason, JavaScript regular expressions are tolerant of syntax errors. For example, `/\w{1, 2/` is a syntax error, but JavaScript doesn't throw the error. It matches strings such as `"a{1, 2"` instead. Such a recovering logic is defined in Annex B.

    The `u` flag disables the recovering logic Annex B defined. As a result, you can find errors early. This is similar to [the strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode).

Therefore, the `u` flag lets us work better with regular expressions.

## 规则详解

This rule aims to enforce the use of `u` flag on regular expressions.

此规则的 **错误** 代码实例：



```js
/*eslint require-unicode-regexp: error */

const a = /aaa/
const b = /bbb/gi
const c = new RegExp("ccc")
const d = new RegExp("ddd", "gi")
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint require-unicode-regexp: error */

const a = /aaa/u
const b = /bbb/giu
const c = new RegExp("ccc", "u")
const d = new RegExp("ddd", "giu")

// This rule ignores RegExp calls if the flags could not be evaluated to a static value.
function f(flags) {
    return new RegExp("eee", flags)
}
```

## 禁用建议

If you don't want to notify regular expressions with no `u` flag, then it's safe to disable this rule.
