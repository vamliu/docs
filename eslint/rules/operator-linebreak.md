---
规则名: operator-linebreak
规则类型: layout
关联规则:
- comma-style
---



When a statement is too long to fit on a single line, line breaks are generally inserted next to the operators separating expressions. The first style coming to mind would be to place the operator at the end of the line, following the English punctuation rules.

```js
var fullHeight = borderTop +
                 innerHeight +
                 borderBottom;
```

Some developers find that placing operators at the beginning of the line makes the code more readable.

```js
var fullHeight = borderTop
               + innerHeight
               + borderBottom;
```

## 规则详解

This rule enforces a consistent linebreak style for operators.

## 配置项

This rule has two options, a string option and an object option.

String option:

* `"after"` requires linebreaks to be placed after the operator
* `"before"` requires linebreaks to be placed before the operator
* `"none"` disallows linebreaks on either side of the operator

Object option:

* `"overrides"` overrides the global setting for specified operators

The default configuration is `"after", { "overrides": { "?": "before", ":": "before" } }`

### after

选项 `"after"` 的 **错误** 代码示例：



```js
/*eslint operator-linebreak: ["error", "after"]*/

foo = 1
+
2;

foo = 1
    + 2;

foo
    = 5;

if (someCondition
    || otherCondition) {
}

answer = everything
  ? 42
  : foo;

class Foo {
    a
        = 1;
    [b]
        = 2;
    [c
    ]
        = 3;
}
```

选项 `"after"` 的 **正确** 代码示例：

::: correct

```js
/*eslint operator-linebreak: ["error", "after"]*/

foo = 1 + 2;

foo = 1 +
      2;

foo =
    5;

if (someCondition ||
    otherCondition) {
}

answer = everything ?
  42 :
  foo;

class Foo {
    a =
        1;
    [b] =
        2;
    [c
    ] =
        3;
    d = 4;
}
```

### before

选项 `"before"` 的 **错误** 代码示例：



```js
/*eslint operator-linebreak: ["error", "before"]*/

foo = 1 +
      2;

foo =
    5;

if (someCondition ||
    otherCondition) {
}

answer = everything ?
  42 :
  foo;

class Foo {
    a =
        1;
    [b] =
        2;
    [c
    ] =
        3;
}
```

选项 `"before"` 的 **正确** 代码示例：

::: correct

```js
/*eslint operator-linebreak: ["error", "before"]*/

foo = 1 + 2;

foo = 1
    + 2;

foo
    = 5;

if (someCondition
    || otherCondition) {
}

answer = everything
  ? 42
  : foo;

class Foo {
    a
        = 1;
    [b]
        = 2;
    [c
    ]
        = 3;
    d = 4;
}
```

### none

选项 `"none"` 的 **错误** 代码示例：



```js
/*eslint operator-linebreak: ["error", "none"]*/

foo = 1 +
      2;

foo = 1
    + 2;

if (someCondition ||
    otherCondition) {
}

if (someCondition
    || otherCondition) {
}

answer = everything
  ? 42
  : foo;

answer = everything ?
  42 :
  foo;

class Foo {
    a =
        1;
    [b] =
        2;
    [c
    ] =
        3;
    d
        = 4;
    [e]
        = 5;
    [f
    ]
        = 6;
}
```

选项 `"none"` 的 **正确** 代码示例：

::: correct

```js
/*eslint operator-linebreak: ["error", "none"]*/

foo = 1 + 2;

foo = 5;

if (someCondition || otherCondition) {
}

answer = everything ? 42 : foo;

class Foo {
    a = 1;
    [b] = 2;
    [c
    ] = 3;
    d = 4;
    [e] = 5;
    [f
    ] = 6;
}
```

### overrides

Examples of additional **incorrect** code for this rule with the `{ "overrides": { "+=": "before" } }` option:



```js
/*eslint operator-linebreak: ["error", "after", { "overrides": { "+=": "before" } }]*/

var thing = 'thing';
thing +=
  's';
```

Examples of additional **correct** code for this rule with the `{ "overrides": { "+=": "before" } }` option:

::: correct

```js
/*eslint operator-linebreak: ["error", "after", { "overrides": { "+=": "before" } }]*/

var thing = 'thing';
thing
  += 's';
```

Examples of additional **correct** code for this rule with the `{ "overrides": { "?": "ignore", ":": "ignore" } }` option:

::: correct

```js
/*eslint operator-linebreak: ["error", "after", { "overrides": { "?": "ignore", ":": "ignore" } }]*/

answer = everything ?
  42
  : foo;

answer = everything
  ?
  42
  :
  foo;
```

选项 `"after", { "overrides": { "?": "before", ":": "before" } }`  默认值的 **错误** 代码示例：



```js
/*eslint operator-linebreak: ["error", "after", { "overrides": { "?": "before", ":": "before" } }]*/

foo = 1
+
2;

foo = 1
    + 2;

foo
    = 5;

if (someCondition
    || otherCondition) {
}

answer = everything ?
  42 :
  foo;
```

选项 `"after", { "overrides": { "?": "before", ":": "before" } }` 默认值的 **正确** 代码示例：

::: correct

```js
/*eslint operator-linebreak: ["error", "after", { "overrides": { "?": "before", ":": "before" } }]*/

foo = 1 + 2;

foo = 1 +
      2;

foo =
    5;

if (someCondition ||
    otherCondition) {
}

answer = everything
  ? 42
  : foo;
```

## 禁用建议

If your project will not be using a common operator line break style, turn this rule off.
