---
规则名: dot-notation
规则类型: suggestion
---



In JavaScript, one can access properties using the dot notation (`foo.bar`) or square-bracket notation (`foo["bar"]`). However, the dot notation is often preferred because it is easier to read, less verbose, and works better with aggressive JavaScript minimizers.

```js
foo["bar"];
```

## 规则详解

This rule is aimed at maintaining code consistency and improving code readability by encouraging use of the dot notation style whenever possible. As such, it will warn when it encounters an unnecessary use of square-bracket notation.

此规则的 **错误** 代码实例：

```js
/*eslint dot-notation: "error"*/

var x = foo["bar"];
```

此规则的 **正确** 代码实例：

```js
/*eslint dot-notation: "error"*/

var x = foo.bar;

var x = foo[bar];    // Property name is a variable, square-bracket notation required
```

## 配置项

This rule accepts a single options argument:

* Set the `allowKeywords` option to `false` (default is `true`) to follow ECMAScript version 3 compatible style, avoiding dot notation for reserved word properties.
* Set the `allowPattern` option to a regular expression string to allow bracket notation for property names that match a pattern (by default, no pattern is tested).

### allowKeywords

选项 `{ "allowKeywords": false }` 的 **正确** 代码示例：

```js
/*eslint dot-notation: ["error", { "allowKeywords": false }]*/

var foo = { "class": "CS 101" }
var x = foo["class"]; // Property name is a reserved word, square-bracket notation required
```

Examples of additional **correct** code for the `{ "allowKeywords": false }` option:

```js
/*eslint dot-notation: ["error", { "allowKeywords": false }]*/

class C {
    #in;
    foo() {
        this.#in; // Dot notation is required for private identifiers
    }
}
```

### allowPattern

For example, when preparing data to be sent to an external API, it is often required to use property names that include underscores.  If the `camelcase` rule is in effect, these [snake case](https://en.wikipedia.org/wiki/Snake_case) properties would not be allowed.  By providing an `allowPattern` to the `dot-notation` rule, these snake case properties can be accessed with bracket notation.

选项 sample `{ "allowPattern": "^[a-z]+(_[a-z]+)+$" }` 的 **正确** 代码示例：

```js
/*eslint camelcase: "error"*/
/*eslint dot-notation: ["error", { "allowPattern": "^[a-z]+(_[a-z]+)+$" }]*/

var data = {};
data.foo_bar = 42;

var data = {};
data["fooBar"] = 42;

var data = {};
data["foo_bar"] = 42; // no warning
```
