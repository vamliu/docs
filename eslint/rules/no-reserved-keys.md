---
规则名: no-reserved-keys

深入了解:
- https://kangax.github.io/compat-table/es5/#Reserved_words_as_property_names
---

Disallows unquoted reserved words as property names in object literals.

(removed) This rule was **removed** in ESLint v1.0 and **replaced** by the [quote-props](quote-props) rule.

ECMAScript 3 described as series of keywords and reserved words, such as `if` and `public`, that are used or intended to be used for a core language feature. The specification also indicated that these keywords and reserved words could not be used as object property names without being enclosed in strings. An error occurs in an ECMAScript 3 environment when you use a keyword or reserved word in an object literal. For example:

```js
var values = {
    enum: ["red", "blue", "green"]  // throws an error in ECMAScript 3
}
```

In this code, `enum` is used as an object key and will throw an error in an ECMAScript 3 environment (such as Internet Explorer 8).

ECMAScript 5 loosened the restriction such that keywords and reserved words can be used as object keys without causing an error. However, any code that needs to run in ECMAScript 3 still needs to avoid using keywords and reserved words as keys.

## 规则详解

This rule is aimed at eliminating the use of ECMAScript 3 keywords and reserved words as object literal keys. As such, it warns whenever an object key would throw an error in an ECMAScript 3 environment.

此规则的 **错误** 代码实例：



```js
var superman = {
    class: "Superhero",
    private: "Clark Kent"
};

var values = {
    enum: ["red", "blue", "green"]
};
```

此规则的 **正确** 代码实例：

::: correct

```js
var superman = {
    "class": "Superhero",
    "private": "Clark Kent"
};

var values = {
    "enum": ["red", "blue", "green"]
};
```

## 禁用建议

If your code is only going to be executed in an ECMAScript 5 or higher environment, then you can safely leave this rule off.
