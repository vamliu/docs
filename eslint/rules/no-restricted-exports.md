---
规则名: no-restricted-exports
规则类型: suggestion
---


In a project, certain names may be disallowed from being used as exported names for various reasons.

## 规则详解

This rule disallows specified names from being used as exported names.

## 配置项

By default, this rule doesn't disallow any names. Only the names you specify in the configuration will be disallowed.

This rule has an object option:

* `"restrictedNamedExports"` is an array of strings, where each string is a name to be restricted.

此规则的 **错误** 代码实例：



```js
/*eslint no-restricted-exports: ["error", {
    "restrictedNamedExports": ["foo", "bar", "Baz", "a", "b", "c", "d", "e", "👍"]
}]*/

export const foo = 1;

export function bar() {}

export class Baz {}

const a = {};
export { a };

function someFunction() {}
export { someFunction as b };

export { c } from "some_module";

export { "d" } from "some_module";

export { something as e } from "some_module";

export { "👍" } from "some_module";
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-restricted-exports: ["error", {
    "restrictedNamedExports": ["foo", "bar", "Baz", "a", "b", "c", "d", "e", "👍"]
}]*/

export const quux = 1;

export function myFunction() {}

export class MyClass {}

const a = {};
export { a as myObject };

function someFunction() {}
export { someFunction };

export { c as someName } from "some_module";

export { "d" as " d " } from "some_module";

export { something } from "some_module";

export { "👍" as thumbsUp } from "some_module";
```

### Default exports

By design, this rule doesn't disallow `export default` declarations. If you configure `"default"` as a restricted name, that restriction will apply only to named export declarations.

Examples of additional **incorrect** code for this rule:



```js
/*eslint no-restricted-exports: ["error", { "restrictedNamedExports": ["default"] }]*/

function foo() {}

export { foo as default };
```



```js
/*eslint no-restricted-exports: ["error", { "restrictedNamedExports": ["default"] }]*/

export { default } from "some_module";
```

Examples of additional **correct** code for this rule:

::: correct

```js
/*eslint no-restricted-exports: ["error", { "restrictedNamedExports": ["default", "foo"] }]*/

export default function foo() {}
```

## 已知局限

This rule doesn't inspect the content of source modules in re-export declarations. In particular, if you are re-exporting everything from another module's export, that export may include a restricted name. This rule cannot detect such cases.

```js

//----- some_module.js -----
export function foo() {}

//----- my_module.js -----
/*eslint no-restricted-exports: ["error", { "restrictedNamedExports": ["foo"] }]*/

export * from "some_module"; // allowed, although this declaration exports "foo" from my_module
```
