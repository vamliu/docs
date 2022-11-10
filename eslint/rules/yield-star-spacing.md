---
规则名: yield-star-spacing
规则类型: layout
深入了解:
- https://leanpub.com/understandinges6/read/#leanpub-auto-generators
---



## 规则详解

This rule enforces spacing around the `*` in `yield*` expressions.

## 配置项

The rule takes one option, an object, which has two keys `before` and `after` having boolean values `true` or `false`.

* `before` enforces spacing between the `yield` and the `*`.
  If `true`, a space is required, otherwise spaces are disallowed.

* `after` enforces spacing between the `*` and the argument.
  If it is `true`, a space is required, otherwise spaces are disallowed.

The default is `{"before": false, "after": true}`.

```json
"yield-star-spacing": ["error", {"before": true, "after": false}]
```

The option also has a string shorthand:

* `{"before": false, "after": true}` → `"after"`
* `{"before": true, "after": false}` → `"before"`
* `{"before": true, "after": true}` → `"both"`
* `{"before": false, "after": false}` → `"neither"`

```json
"yield-star-spacing": ["error", "after"]
```

## Examples

### after

选项 `"after"` 默认值的 **正确** 代码示例：

::: correct

```js
/*eslint yield-star-spacing: ["error", "after"]*/
/*eslint-env es6*/

function* generator() {
  yield* other();
}
```

### before

选项 `"before"` 的 **正确** 代码示例：

::: correct

```js
/*eslint yield-star-spacing: ["error", "before"]*/
/*eslint-env es6*/

function *generator() {
  yield *other();
}
```

### both

选项 `"both"` 的 **正确** 代码示例：

::: correct

```js
/*eslint yield-star-spacing: ["error", "both"]*/
/*eslint-env es6*/

function * generator() {
  yield * other();
}
```

### neither

选项 `"neither"` 的 **正确** 代码示例：

::: correct

```js
/*eslint yield-star-spacing: ["error", "neither"]*/
/*eslint-env es6*/

function*generator() {
  yield*other();
}
```

## 禁用建议

If your project will not be using generators or you are not concerned with spacing consistency, you do not need this rule.
