---
规则名: space-unary-ops
规则类型: layout
---



Some style guides require or disallow spaces before or after unary operators. This is mainly a stylistic issue, however, some JavaScript expressions can be written without spacing which makes it harder to read and maintain.

## 规则详解

This rule enforces consistency regarding the spaces after `words` unary operators and after/before `nonwords` unary operators.

For `words` operators, this rule only applies when a space is not syntactically required. For instance, `delete obj.foo` requires the space and will not be considered by this rule. The equivalent `delete(obj.foo)` has an optional space (`delete (obj.foo)`), therefore this rule will apply to it.

Examples of unary `words` operators:

```js
// new
var joe = new Person();

// delete
var obj = {
    foo: 'bar'
};
delete obj.foo;

// typeof
typeof {} // object

// void
void 0 // undefined
```

Examples of unary `nonwords` operators:

```js
if ([1,2,3].indexOf(1) !== -1) {};
foo = --foo;
bar = bar++;
baz = !foo;
qux = !!baz;
```

## 配置项

This rule has three options:

* `words` - applies to unary word operators such as: `new`, `delete`, `typeof`, `void`, `yield`
* `nonwords` - applies to unary operators such as: `-`, `+`, `--`, `++`, `!`, `!!`
* `overrides` - specifies overwriting usage of spacing for each
  operator, word or non word. This is empty by default, but can be used
  to enforce or disallow spacing around operators. For example:

```js
    "space-unary-ops": [
        2, {
          "words": true,
          "nonwords": false,
          "overrides": {
            "new": false,
            "++": true
          }
    }]
```

In this case, spacing will be disallowed after a `new` operator and required before/after a `++` operator.

选项 `{"words": true, "nonwords": false}`  默认值的 **错误** 代码示例：



```js
/*eslint space-unary-ops: "error"*/

typeof!foo;

void{foo:0};

new[foo][0];

delete(foo.bar);

++ foo;

foo --;

- foo;

+ "3";
```



```js
/*eslint space-unary-ops: "error"*/
/*eslint-env es6*/

function *foo() {
    yield(0)
}
```



```js
/*eslint space-unary-ops: "error"*/

async function foo() {
    await(bar);
}
```

选项 `{"words": true, "nonwords": false}` 的 **正确** 代码示例：

::: correct

```js
/*eslint space-unary-ops: "error"*/

// Word unary operator "typeof" is followed by a whitespace.
typeof !foo;

// Word unary operator "void" is followed by a whitespace.
void {foo:0};

// Word unary operator "new" is followed by a whitespace.
new [foo][0];

// Word unary operator "delete" is followed by a whitespace.
delete (foo.bar);

// Unary operator "++" is not followed by whitespace.
++foo;

// Unary operator "--" is not preceded by whitespace.
foo--;

// Unary operator "-" is not followed by whitespace.
-foo;

// Unary operator "+" is not followed by whitespace.
+"3";
```

::: correct

```js
/*eslint space-unary-ops: "error"*/
/*eslint-env es6*/

function *foo() {
    yield (0)
}
```

::: correct

```js
/*eslint space-unary-ops: "error"*/

async function foo() {
    await (bar);
}
```
