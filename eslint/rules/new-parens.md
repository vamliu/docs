---
规则名: new-parens
规则类型: layout
---



JavaScript allows the omission of parentheses when invoking a function via the `new` keyword and the constructor has no arguments. However, some coders believe that omitting the parentheses is inconsistent with the rest of the language and thus makes code less clear.

```js
var person = new Person;
```

## 规则详解

This rule can enforce or disallow parentheses when invoking a constructor with no arguments using the `new` keyword.

## 配置项

This rule takes one option.

* `"always"` enforces parenthesis after a new constructor with no arguments (default)
* `"never"` enforces no parenthesis after a new constructor with no arguments

### always

选项 `"always"` 的 **错误** 代码示例：



```js
/*eslint new-parens: "error"*/

var person = new Person;
var person = new (Person);
```

选项 `"always"` 的 **正确** 代码示例：

::: correct

```js
/*eslint new-parens: "error"*/

var person = new Person();
var person = new (Person)();
```

### never

选项 `"never"` 的 **错误** 代码示例：



```js
/*eslint new-parens: ["error", "never"]*/

var person = new Person();
var person = new (Person)();
```

选项 `"never"` 的 **正确** 代码示例：

::: correct

```js
/*eslint new-parens: ["error", "never"]*/

var person = new Person;
var person = (new Person);
var person = new Person("Name");
```
