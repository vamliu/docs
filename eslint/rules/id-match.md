---
规则名: id-match
规则类型: suggestion
---


> "There are only two hard things in Computer Science: cache invalidation and naming things." — Phil Karlton

Naming things consistently in a project is an often underestimated aspect of code creation.
When done correctly, it can save your team hours of unnecessary head scratching and misdirections.
This rule allows you to precisely define and enforce the variables and function names on your team should use.
No more limiting yourself to camelCase, snake_case, PascalCase or oHungarianNotation. Id-match has all your needs covered!

## 规则详解

This rule requires identifiers in assignments and `function` definitions to match a specified regular expression.

## 配置项

This rule has a string option for the specified regular expression.

For example, to enforce a camelcase naming convention:

```json
{
    "id-match": ["error", "^[a-z]+([A-Z][a-z]+)*$"]
}
```

选项 `"^[a-z]+([A-Z][a-z]+)*$"` 的 **错误** 代码示例：



```js
/*eslint id-match: ["error", "^[a-z]+([A-Z][a-z]+)*$"]*/

var my_favorite_color = "#112C85";
var _myFavoriteColor  = "#112C85";
var myFavoriteColor_  = "#112C85";
var MY_FAVORITE_COLOR = "#112C85";
function do_something() {
    // ...
}

obj.do_something = function() {
    // ...
};

class My_Class {}

class myClass {
    do_something() {}
}

class myClass {
    #do_something() {}
}
```

选项 `"^[a-z]+([A-Z][a-z]+)*$"` 的 **正确** 代码示例：

::: correct

```js
/*eslint id-match: ["error", "^[a-z]+([A-Z][a-z]+)*$"]*/

var myFavoriteColor   = "#112C85";
var foo = bar.baz_boom;
var foo = { qux: bar.baz_boom };
do_something();
var obj = {
    my_pref: 1
};

class myClass {}

class myClass {
    doSomething() {}
}

class myClass {
    #doSomething() {}
}
```

This rule has an object option:

* `"properties": false` (default) does not check object properties
* `"properties": true` requires object literal properties and member expression assignment properties to match the specified regular expression
* `"classFields": false` (default) does not class field names
* `"classFields": true` requires class field names to match the specified regular expression
* `"onlyDeclarations": false` (default) requires all variable names to match the specified regular expression
* `"onlyDeclarations": true` requires only `var`, `function`, and `class` declarations to match the specified regular expression
* `"ignoreDestructuring": false` (default) enforces `id-match` for destructured identifiers
* `"ignoreDestructuring": true` does not check destructured identifiers

### properties

选项 `"^[a-z]+([A-Z][a-z]+)*$", { "properties": true }`  的 **错误** 代码示例：



```js
/*eslint id-match: ["error", "^[a-z]+([A-Z][a-z]+)*$", { "properties": true }]*/

var obj = {
    my_pref: 1
};
```

### classFields

选项 `"^[a-z]+([A-Z][a-z]+)*$", { "classFields": true }`  的 **错误** 代码示例：



```js
/*eslint id-match: ["error", "^[a-z]+([A-Z][a-z]+)*$", { "properties": true }]*/

class myClass {
    my_pref = 1;
}

class myClass {
    #my_pref = 1;
}
```

### onlyDeclarations

选项 `"^[a-z]+([A-Z][a-z]+)*$", { "onlyDeclarations": true }`  的 **正确** 代码示例：

::: correct

```js
/*eslint id-match: [2, "^[a-z]+([A-Z][a-z]+)*$", { "onlyDeclarations": true }]*/

do_something(__dirname);
```

### ignoreDestructuring: false

选项 `"^[^_]+$", { "ignoreDestructuring": false }`  默认值的 **错误** 代码示例：



```js
/*eslint id-match: [2, "^[^_]+$", { "ignoreDestructuring": false }]*/

var { category_id } = query;

var { category_id = 1 } = query;

var { category_id: category_id } = query;

var { category_id: category_alias } = query;

var { category_id: categoryId, ...other_props } = query;
```

### ignoreDestructuring: true

选项 `"^[^_]+$", { "ignoreDestructuring": true }` 的 **错误** 代码示例：



```js
/*eslint id-match: [2, "^[^_]+$", { "ignoreDestructuring": true }]*/

var { category_id: category_alias } = query;

var { category_id, ...other_props } = query;
```

选项 `"^[^_]+$", { "ignoreDestructuring": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint id-match: [2, "^[^_]+$", { "ignoreDestructuring": true }]*/

var { category_id } = query;

var { category_id = 1 } = query;

var { category_id: category_id } = query;
```

## 禁用建议

If you don't want to enforce any particular naming convention for all identifiers, or your naming convention is too complex to be enforced by configuring this rule, then you should not enable this rule.
