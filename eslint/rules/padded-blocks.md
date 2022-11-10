---
规则名: padded-blocks
规则类型: layout
关联规则:
- lines-between-class-members
- padding-line-between-statements
---



Some style guides require block statements to start and end with blank lines. The goal is
to improve readability by visually separating the block content and the surrounding code.

```js
if (a) {

    b();

}
```

Since it's good to have a consistent code style, you should either always write
padded blocks or never do it.

## 规则详解

This rule enforces consistent empty line padding within blocks.

## 配置项

This rule has two options, the first one can be a string option or an object option.
The second one is an object option, it can allow exceptions.

### First option

String option:

* `"always"` (default) requires empty lines at the beginning and ending of block statements, function bodies, class static blocks, classes, and `switch` statements.
* `"never"` disallows empty lines at the beginning and ending of block statements, function bodies, class static blocks, classes, and `switch` statements.

Object option:

* `"blocks"` require or disallow padding within block statements, function bodies, and class static blocks
* `"classes"` require or disallow padding within classes
* `"switches"` require or disallow padding within `switch` statements

### Second option

* `"allowSingleLineBlocks": true` allows single-line blocks

### always

选项 `"always"`  默认值的 **错误** 代码示例：



```js
/*eslint padded-blocks: ["error", "always"]*/

if (a) {
    b();
}

if (a) { b(); }

if (a)
{
    b();
}

if (a) {
    b();

}

if (a) {
    // comment
    b();

}

class C {
    static {
        a();
    }
}
```

选项 `"always"` 默认值的 **正确** 代码示例：

::: correct

```js
/*eslint padded-blocks: ["error", "always"]*/

if (a) {

    b();

}

if (a)
{

    b();

}

if (a) {

    // comment
    b();

}

class C {

    static {

        a();

    }

}
```

### never

选项 `"never"` 的 **错误** 代码示例：



```js
/*eslint padded-blocks: ["error", "never"]*/

if (a) {

    b();

}

if (a)
{

    b();

}

if (a) {

    b();
}

if (a) {
    b();

}

class C {

    static {

        a();

    }

}
```

选项 `"never"` 的 **正确** 代码示例：

::: correct

```js
/*eslint padded-blocks: ["error", "never"]*/

if (a) {
    b();
}

if (a)
{
    b();
}

class C {
    static {
        a();
    }
}
```

### blocks

选项 `{ "blocks": "always" }` 的 **错误** 代码示例：



```js
/*eslint padded-blocks: ["error", { "blocks": "always" }]*/

if (a) {
    b();
}

if (a) { b(); }

if (a)
{
    b();
}

if (a) {

    b();
}

if (a) {
    b();

}

if (a) {
    // comment
    b();

}

class C {

    static {
        a();
    }

}
```

选项 `{ "blocks": "always" }` 的 **正确** 代码示例：

::: correct

```js
/*eslint padded-blocks: ["error", { "blocks": "always" }]*/

if (a) {

    b();

}

if (a)
{

    b();

}

if (a) {

    // comment
    b();

}

class C {

    static {

        a();

    }

}

class D {
    static {

        a();

    }

}
```

选项 `{ "blocks": "never" }` 的 **错误** 代码示例：



```js
/*eslint padded-blocks: ["error", { "blocks": "never" }]*/

if (a) {

    b();

}

if (a)
{

    b();

}

if (a) {

    b();
}

if (a) {
    b();

}

class C {
    static {

        a();

    }
}
```

选项 `{ "blocks": "never" }` 的 **正确** 代码示例：

::: correct

```js
/*eslint padded-blocks: ["error", { "blocks": "never" }]*/

if (a) {
    b();
}

if (a)
{
    b();
}

class C {
    static {
        a();
    }
}

class D {

    static {
        a();
    }

}
```

### classes

选项 `{ "classes": "always" }` 的 **错误** 代码示例：



```js
/*eslint padded-blocks: ["error", { "classes": "always" }]*/

class  A {
    constructor(){
    }
}
```

选项 `{ "classes": "always" }` 的 **正确** 代码示例：

::: correct

```js
/*eslint padded-blocks: ["error", { "classes": "always" }]*/

class  A {

    constructor(){
    }

}
```

选项 `{ "classes": "never" }` 的 **错误** 代码示例：



```js
/*eslint padded-blocks: ["error", { "classes": "never" }]*/

class  A {

    constructor(){
    }

}
```

选项 `{ "classes": "never" }` 的 **正确** 代码示例：

::: correct

```js
/*eslint padded-blocks: ["error", { "classes": "never" }]*/

class  A {
    constructor(){
    }
}
```

### switches

选项 `{ "switches": "always" }` 的 **错误** 代码示例：



```js
/*eslint padded-blocks: ["error", { "switches": "always" }]*/

switch (a) {
    case 0: foo();
}
```

选项 `{ "switches": "always" }` 的 **正确** 代码示例：

::: correct

```js
/*eslint padded-blocks: ["error", { "switches": "always" }]*/

switch (a) {

    case 0: foo();

}

if (a) {
    b();
}
```

选项 `{ "switches": "never" }` 的 **错误** 代码示例：



```js
/*eslint padded-blocks: ["error", { "switches": "never" }]*/

switch (a) {

    case 0: foo();

}
```

选项 `{ "switches": "never" }` 的 **正确** 代码示例：

::: correct

```js
/*eslint padded-blocks: ["error", { "switches": "never" }]*/

switch (a) {
    case 0: foo();
}

if (a) {

    b();

}
```

### always + allowSingleLineBlocks

选项 `"always", {"allowSingleLineBlocks": true}`  的 **错误** 代码示例：



```js
/*eslint padded-blocks: ["error", "always", { allowSingleLineBlocks: true }]*/

if (a) {
    b();
}

if (a) {

    b();
}

if (a) {
    b();

}
```

选项 `"always", {"allowSingleLineBlocks": true}`  的 **正确** 代码示例：

::: correct

```js
/*eslint padded-blocks: ["error", "always", { allowSingleLineBlocks: true }]*/

if (a) { b(); }

if (a) {

    b();

}
```

## 禁用建议

You can turn this rule off if you are not concerned with the consistency of padding within blocks.
