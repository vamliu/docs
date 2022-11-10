---
规则名: function-call-argument-newline
规则类型: layout
关联规则:
- function-paren-newline
- func-call-spacing
- object-property-newline
- array-element-newline
---



A number of style guides require or disallow line breaks between arguments of a function call.

## 规则详解

This rule enforces line breaks between arguments of a function call.

## 配置项

This rule has a string option:

* `"always"` (default) requires line breaks between arguments
* `"never"` disallows line breaks between arguments
* `"consistent"` requires consistent usage of line breaks between arguments

### always

选项 `"always"`  默认值的 **错误** 代码示例：



```js
/*eslint function-call-argument-newline: ["error", "always"]*/

foo("one", "two", "three");

bar("one", "two", {
    one: 1,
    two: 2
});

baz("one", "two", (x) => {
    console.log(x);
});
```

选项 `"always"` 默认值的 **正确** 代码示例：

::: correct

```js
/*eslint function-call-argument-newline: ["error", "always"]*/

foo(
    "one",
    "two",
    "three"
);

bar(
    "one",
    "two",
    { one: 1, two: 2 }
);
// or
bar(
    "one",
    "two",
    {
        one: 1,
        two: 2
    }
);

baz(
    "one",
    "two",
    (x) => {
        console.log(x);
    }
);
```

### never

选项 `"never"` 的 **错误** 代码示例：



```js
/*eslint function-call-argument-newline: ["error", "never"]*/

foo(
    "one",
    "two", "three"
);

bar(
    "one",
    "two", {
        one: 1,
        two: 2
    }
);

baz(
    "one",
    "two", (x) => {
        console.log(x);
    }
);
```

选项 `"never"` 的 **正确** 代码示例：

::: correct

```js
/*eslint function-call-argument-newline: ["error", "never"]*/

foo("one", "two", "three");
// or
foo(
    "one", "two", "three"
);

bar("one", "two", { one: 1, two: 2 });
// or
bar("one", "two", {
    one: 1,
    two: 2
});

baz("one", "two", (x) => {
    console.log(x);
});
```

### consistent

选项 `"consistent"` 的 **错误** 代码示例：



```js
/*eslint function-call-argument-newline: ["error", "consistent"]*/

foo("one", "two",
    "three");
//or
foo("one",
    "two", "three");

bar("one", "two",
    { one: 1, two: 2}
);

baz("one", "two",
    (x) => { console.log(x); }
);
```

选项 `"consistent"` 的 **正确** 代码示例：

::: correct

```js
/*eslint function-call-argument-newline: ["error", "consistent"]*/

foo("one", "two", "three");
// or
foo(
    "one",
    "two",
    "three"
);

bar("one", "two", {
    one: 1,
    two: 2
});
// or
bar(
    "one",
    "two",
    { one: 1, two: 2 }
);
// or
bar(
    "one",
    "two",
    {
        one: 1,
        two: 2
    }
);

baz("one", "two", (x) => {
    console.log(x);
});
// or
baz(
    "one",
    "two",
    (x) => {
        console.log(x);
    }
);
```

## 禁用建议

If you don't want to enforce line breaks between arguments, don't enable this rule.
