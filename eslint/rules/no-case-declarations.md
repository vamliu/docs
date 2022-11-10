---
规则名: no-case-declarations
规则类型: suggestion
关联规则:
- no-fallthrough
---



This rule disallows lexical declarations (`let`, `const`, `function` and `class`)
in `case`/`default` clauses. The reason is that the lexical declaration is visible
in the entire switch block but it only gets initialized when it is assigned, which
will only happen if the case where it is defined is reached.

To ensure that the lexical declaration only applies to the current case clause
wrap your clauses in blocks.

## 规则详解

This rule aims to prevent access to uninitialized lexical bindings as well as accessing hoisted functions across case clauses.

此规则的 **错误** 代码实例：



```js
/*eslint no-case-declarations: "error"*/
/*eslint-env es6*/

switch (foo) {
    case 1:
        let x = 1;
        break;
    case 2:
        const y = 2;
        break;
    case 3:
        function f() {}
        break;
    default:
        class C {}
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-case-declarations: "error"*/
/*eslint-env es6*/

// Declarations outside switch-statements are valid
const a = 0;

switch (foo) {
    // The following case clauses are wrapped into blocks using brackets
    case 1: {
        let x = 1;
        break;
    }
    case 2: {
        const y = 2;
        break;
    }
    case 3: {
        function f() {}
        break;
    }
    case 4:
        // Declarations using var without brackets are valid due to function-scope hoisting
        var z = 4;
        break;
    default: {
        class C {}
    }
}
```

## 禁用建议

If you depend on fall through behavior and want access to bindings introduced in the case block.
