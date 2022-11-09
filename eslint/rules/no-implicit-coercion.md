---
规则名: no-implicit-coercion
布局: doc
规则类型: suggestion
---



In JavaScript, there are a lot of different ways to convert value types.
Some of them might be hard to read and understand.

Such as:

```js
var b = !!foo;
var b = ~foo.indexOf(".");
var n = +foo;
var n = 1 * foo;
var s = "" + foo;
foo += ``;
```

Those can be replaced with the following code:

```js
var b = Boolean(foo);
var b = foo.indexOf(".") !== -1;
var n = Number(foo);
var n = Number(foo);
var s = String(foo);
foo = String(foo);
```

## 规则详解

This rule is aimed to flag shorter notations for the type conversion, then suggest a more self-explanatory notation.

## 配置项

This rule has three main options and one override option to allow some coercions as required.

* `"boolean"` (`true` by default) - When this is `true`, this rule warns shorter type conversions for `boolean` type.
* `"number"` (`true` by default) - When this is `true`, this rule warns shorter type conversions for `number` type.
* `"string"` (`true` by default) - When this is `true`, this rule warns shorter type conversions for `string` type.
* `"disallowTemplateShorthand"` (`false` by default) - When this is `true`, this rule warns `string` type conversions using `${expression}` form.
* `"allow"` (`empty` by default) - Each entry in this array can be one of `~`, `!!`, `+` or `*` that are to be allowed.

Note that operator `+` in `allow` list would allow `+foo` (number coercion) as well as `"" + foo` (string coercion).

### boolean

选项 default `{ "boolean": true }` 的 **错误** 代码示例：



```js
/*eslint no-implicit-coercion: "error"*/

var b = !!foo;
var b = ~foo.indexOf(".");
// bitwise not is incorrect only with `indexOf`/`lastIndexOf` method calling.
```

选项 default `{ "boolean": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-implicit-coercion: "error"*/

var b = Boolean(foo);
var b = foo.indexOf(".") !== -1;

var n = ~foo; // This is a just bitwise not.
```

### number

选项 default `{ "number": true }` 的 **错误** 代码示例：



```js
/*eslint no-implicit-coercion: "error"*/

var n = +foo;
var n = 1 * foo;
```

选项 default `{ "number": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-implicit-coercion: "error"*/

var n = Number(foo);
var n = parseFloat(foo);
var n = parseInt(foo, 10);
```

### string

选项 default `{ "string": true }` 的 **错误** 代码示例：



```js
/*eslint no-implicit-coercion: "error"*/

var s = "" + foo;
var s = `` + foo;
foo += "";
foo += ``;
```

选项 default `{ "string": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-implicit-coercion: "error"*/

var s = String(foo);
foo = String(foo);
```

### disallowTemplateShorthand

This option is **not** affected by the `string` option.

选项 `{ "disallowTemplateShorthand": true }` 的 **错误** 代码示例：



```js
/*eslint no-implicit-coercion: ["error", { "disallowTemplateShorthand": true }]*/

var s = `${foo}`;
```

选项 `{ "disallowTemplateShorthand": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-implicit-coercion: ["error", { "disallowTemplateShorthand": true }]*/

var s = String(foo);

var s = `a${foo}`;

var s = `${foo}b`;

var s = `${foo}${bar}`;

var s = tag`${foo}`;
```

选项 default `{ "disallowTemplateShorthand": false }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-implicit-coercion: ["error", { "disallowTemplateShorthand": false }]*/

var s = `${foo}`;
```

### allow

Using `allow` list, we can override and allow specific operators.

选项 sample `{ "allow": ["!!", "~"] }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-implicit-coercion: [2, { "allow": ["!!", "~"] } ]*/

var b = !!foo;
var b = ~foo.indexOf(".");
```

## 使用建议

If you don't want to be notified about shorter notations for the type conversion, you can safely disable this rule.
