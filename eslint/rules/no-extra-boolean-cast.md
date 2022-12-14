---
规则名: no-extra-boolean-cast
规则类型: suggestion
---





In contexts such as an `if` statement's test where the result of the expression will already be coerced to a Boolean, casting to a Boolean via double negation (`!!`) or a `Boolean` call is unnecessary. For example, these `if` statements are equivalent:

```js
if (!!foo) {
    // ...
}

if (Boolean(foo)) {
    // ...
}

if (foo) {
    // ...
}
```

## 规则详解

This rule disallows unnecessary boolean casts.

此规则的 **错误** 代码实例：



```js
/*eslint no-extra-boolean-cast: "error"*/

var foo = !!!bar;

var foo = !!bar ? baz : bat;

var foo = Boolean(!!bar);

var foo = new Boolean(!!bar);

if (!!foo) {
    // ...
}

if (Boolean(foo)) {
    // ...
}

while (!!foo) {
    // ...
}

do {
    // ...
} while (Boolean(foo));

for (; !!foo; ) {
    // ...
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-extra-boolean-cast: "error"*/

var foo = !!bar;
var foo = Boolean(bar);

function foo() {
    return !!bar;
}

var foo = bar ? !!baz : !!bat;
```

## 配置项

This rule has an object option:

* `"enforceForLogicalOperands"` when set to `true`, in addition to checking default contexts, checks whether the extra boolean cast is contained within a logical expression. Default is `false`, meaning that this rule by default does not warn about extra booleans cast inside logical expression.

### enforceForLogicalOperands

Examples of **incorrect** code for this rule with `"enforceForLogicalOperands"` option set to `true`:



```js
/*eslint no-extra-boolean-cast: ["error", {"enforceForLogicalOperands": true}]*/

if (!!foo || bar) {
    //...
}

while (!!foo && bar) {
    //...
}

if ((!!foo || bar) && baz) {
    //...
}

foo && Boolean(bar) ? baz : bat

var foo = new Boolean(!!bar || baz)
```

Examples of **correct** code for this rule with `"enforceForLogicalOperands"` option set to `true`:

::: correct

```js
/*eslint no-extra-boolean-cast: ["error", {"enforceForLogicalOperands": true}]*/

if (foo || bar) {
    //...
}

while (foo && bar) {
    //...
}

if ((foo || bar) && baz) {
    //...
}

foo && bar ? baz : bat

var foo = new Boolean(bar || baz)

var foo = !!bar || baz;
```
