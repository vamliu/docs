---
规则名: semi-spacing
规则类型: layout
关联规则:
- semi
- no-extra-semi
- comma-spacing
- block-spacing
- space-in-parens
---



JavaScript allows you to place unnecessary spaces before or after a semicolon.

Disallowing or enforcing space around a semicolon can improve the readability of your program.

```js
var a = "b" ;

var c = "d";var e = "f";
```

## 规则详解

This rule aims to enforce spacing around a semicolon. This rule prevents the use of spaces before a semicolon in expressions.

This rule doesn't check spacing in the following cases:

* The spacing after the semicolon if it is the first token in the line.

* The spacing before the semicolon if it is after an opening parenthesis (`(` or `{`), or the spacing after the semicolon if it is before a closing parenthesis (`)` or `}`). That spacing is checked by `space-in-parens` or `block-spacing`.

* The spacing around the semicolon in a for loop with an empty condition (`for(;;)`).

## 配置项

The rule takes one option, an object, which has two keys `before` and `after` having boolean values `true` or `false`.
If `before` is `true`, space is enforced before semicolons and if it's `false`, space is disallowed before semicolons.
If `after` is `true`, space is enforced after semicolons and if it's `false`, space is disallowed after semicolons.
The `after` option will be only applied if a semicolon is not at the end of line.

The default is `{"before": false, "after": true}`.

```json
    "semi-spacing": ["error", {"before": false, "after": true}]
```

### `{"before": false, "after": true}`

This is the default option. It enforces spacing after semicolons and disallows spacing before semicolons.

此规则的 **错误** 代码实例：



```js
/*eslint semi-spacing: "error"*/

var foo ;
var foo;var bar;
throw new Error("error") ;
while (a) { break ; }
for (i = 0 ; i < 10 ; i++) {}
for (i = 0;i < 10;i++) {}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint semi-spacing: "error"*/

var foo;
var foo; var bar;
throw new Error("error");
while (a) { break; }
for (i = 0; i < 10; i++) {}
for (;;) {}
if (true) {;}
;foo();
```

### `{"before": true, "after": false}`

This option enforces spacing before semicolons and disallows spacing after semicolons.

选项 `{"before": true, "after": false}` 的 **错误** 代码示例：



```js
/*eslint semi-spacing: ["error", { "before": true, "after": false }]*/

var foo;
var foo ; var bar;
throw new Error("error");
while (a) { break; }
for (i = 0;i < 10;i++) {}
for (i = 0; i < 10; i++) {}
```

选项 `{"before": true, "after": false}` 的 **正确** 代码示例：

::: correct

```js
/*eslint semi-spacing: ["error", { "before": true, "after": false }]*/

var foo ;
var foo ;var bar ;
throw new Error("error") ;
while (a) {break ;}
for (i = 0 ;i < 10 ;i++) {}
```

## 禁用建议

You can turn this rule off if you are not concerned with the consistency of spacing before or after semicolons.
