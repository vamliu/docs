---
规则名: lines-around-comment
规则类型: layout
关联规则:
- space-before-blocks
- spaced-comment
---



Many style guides require empty lines before or after comments. The primary goal
of these rules is to make the comments easier to read and improve readability of the code.

## 规则详解

This rule requires empty lines before and/or after comments. It can be enabled separately for both block (`/*`) and line (`//`) comments. This rule does not apply to comments that appear on the same line as code and does not require empty lines at the beginning or end of a file.

## 配置项

This rule has an object option:

* `"beforeBlockComment": true` (default) requires an empty line before block comments
* `"afterBlockComment": true` requires an empty line after block comments
* `"beforeLineComment": true` requires an empty line before line comments
* `"afterLineComment": true` requires an empty line after line comments
* `"allowBlockStart": true` allows comments to appear at the start of block statements, function bodies, classes, switch statements, and class static blocks
* `"allowBlockEnd": true` allows comments to appear at the end of block statements, function bodies, classes, switch statements, and class static blocks
* `"allowObjectStart": true` allows comments to appear at the start of object literals
* `"allowObjectEnd": true` allows comments to appear at the end of object literals
* `"allowArrayStart": true` allows comments to appear at the start of array literals
* `"allowArrayEnd": true` allows comments to appear at the end of array literals
* `"allowClassStart": true` allows comments to appear at the start of classes
* `"allowClassEnd": true` allows comments to appear at the end of classes
* `"applyDefaultIgnorePatterns"` enables or disables the default comment patterns to be ignored by the rule
* `"ignorePattern"` custom patterns to be ignored by the rule

### beforeBlockComment

选项 `{ "beforeBlockComment": true }`  默认值的 **错误** 代码示例：



```js
/*eslint lines-around-comment: ["error", { "beforeBlockComment": true }]*/

var night = "long";
/* what a great and wonderful day */
var day = "great"
```

选项 `{ "beforeBlockComment": true }` 默认值的 **正确** 代码示例：

::: correct

```js
/*eslint lines-around-comment: ["error", { "beforeBlockComment": true }]*/

var night = "long";

/* what a great and wonderful day */
var day = "great"
```

### afterBlockComment

选项 `{ "afterBlockComment": true }` 的 **错误** 代码示例：



```js
/*eslint lines-around-comment: ["error", { "afterBlockComment": true }]*/

var night = "long";

/* what a great and wonderful day */
var day = "great"
```

选项 `{ "afterBlockComment": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint lines-around-comment: ["error", { "afterBlockComment": true }]*/

var night = "long";

/* what a great and wonderful day */

var day = "great"
```

### beforeLineComment

选项 `{ "beforeLineComment": true }` 的 **错误** 代码示例：



```js
/*eslint lines-around-comment: ["error", { "beforeLineComment": true }]*/

var night = "long";
// what a great and wonderful day
var day = "great"
```

选项 `{ "beforeLineComment": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint lines-around-comment: ["error", { "beforeLineComment": true }]*/

var night = "long";

// what a great and wonderful day
var day = "great"
```

### afterLineComment

选项 `{ "afterLineComment": true }` 的 **错误** 代码示例：



```js
/*eslint lines-around-comment: ["error", { "afterLineComment": true }]*/

var night = "long";
// what a great and wonderful day
var day = "great"
```

选项 `{ "afterLineComment": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint lines-around-comment: ["error", { "afterLineComment": true }]*/

var night = "long";
// what a great and wonderful day

var day = "great"
```

### allowBlockStart

选项 `{ "beforeLineComment": true, "allowBlockStart": true }`  的 **正确** 代码示例：

::: correct

```js
/*eslint lines-around-comment: ["error", { "beforeLineComment": true, "allowBlockStart": true }]*/

function foo(){
    // what a great and wonderful day
    var day = "great"
    return day;
}

if (bar) {
    // what a great and wonderful day
    foo();
}

class C {
    // what a great and wonderful day

    method() {
        // what a great and wonderful day
        foo();
    }

    static {
        // what a great and wonderful day
        foo();
    }
}
```

选项 `{ "beforeBlockComment": true, "allowBlockStart": true }`  的 **正确** 代码示例：

::: correct

```js
/*eslint lines-around-comment: ["error", { "beforeBlockComment": true, "allowBlockStart": true }]*/

function foo(){
    /* what a great and wonderful day */
    var day = "great"
    return day;
}

if (bar) {
    /* what a great and wonderful day */
    foo();
}

class C {
    /* what a great and wonderful day */

    method() {
        /* what a great and wonderful day */
        foo();
    }

    static {
        /* what a great and wonderful day */
        foo();
    }
}

switch (foo) {
  /* what a great and wonderful day */

  case 1:    
    bar();
    break;
}
```

### allowBlockEnd

选项 `{ "afterLineComment": true, "allowBlockEnd": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint lines-around-comment: ["error", { "afterLineComment": true, "allowBlockEnd": true }]*/

function foo(){
    var day = "great"
    return day;
    // what a great and wonderful day
}

if (bar) {
    foo();
    // what a great and wonderful day
}

class C {

    method() {
        foo();
        // what a great and wonderful day
    }

    static {
        foo();
        // what a great and wonderful day
    }

    // what a great and wonderful day
}
```

选项 `{ "afterBlockComment": true, "allowBlockEnd": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint lines-around-comment: ["error", { "afterBlockComment": true, "allowBlockEnd": true }]*/

function foo(){
    var day = "great"
    return day;

    /* what a great and wonderful day */
}

if (bar) {
    foo();

    /* what a great and wonderful day */
}

class C {

    method() {
        foo();

        /* what a great and wonderful day */
    }

    static {
        foo();

        /* what a great and wonderful day */
    }

    /* what a great and wonderful day */
}

switch (foo) {
  case 1:    
    bar();
    break;

  /* what a great and wonderful day */
}
```

### allowClassStart

选项 `{ "beforeLineComment": true, "allowClassStart": false }` 的 **错误** 代码示例：



```js
/*eslint lines-around-comment: ["error", { "beforeLineComment": true, "allowClassStart": false }]*/

class foo {
    // what a great and wonderful day
    day() {}
};
```

选项 `{ "beforeLineComment": true, "allowClassStart": false }` 的 **正确** 代码示例：

::: correct

```js
/*eslint lines-around-comment: ["error", { "beforeLineComment": true, "allowClassStart": false }]*/

class foo {

    // what a great and wonderful day
    day() {}
};
```

选项 `{ "beforeLineComment": true, "allowClassStart": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint lines-around-comment: ["error", { "beforeLineComment": true, "allowClassStart": true }]*/

class foo {
    // what a great and wonderful day
    day() {}
};
```

选项 `{ "beforeBlockComment": true, "allowClassStart": false }` 的 **错误** 代码示例：



```js
/*eslint lines-around-comment: ["error", { "beforeBlockComment": true, "allowClassStart": false }]*/

class foo {
    /* what a great and wonderful day */
    day() {}
};
```

选项 `{ "beforeBlockComment": true, "allowClassStart": false }` 的 **正确** 代码示例：

::: correct

```js
/*eslint lines-around-comment: ["error", { "beforeBlockComment": true, "allowClassStart": false }]*/

class foo {

    /* what a great and wonderful day */
    day() {}
};
```

选项 `{ "beforeBlockComment": true, "allowClassStart": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint lines-around-comment: ["error", { "beforeBlockComment": true, "allowClassStart": true }]*/

class foo {
    /* what a great and wonderful day */
    day() {}
};
```

### allowClassEnd

选项 `{ "afterLineComment": true, "allowClassEnd": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint lines-around-comment: ["error", { "afterLineComment": true, "allowClassEnd": true }]*/

class foo {
    day() {}
    // what a great and wonderful day
};
```

选项 `{ "afterBlockComment": true, "allowClassEnd": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint lines-around-comment: ["error", { "afterBlockComment": true, "allowClassEnd": true }]*/

class foo {
    day() {}

    /* what a great and wonderful day */
};
```

### allowObjectStart

选项 `{ "beforeLineComment": true, "allowObjectStart": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint lines-around-comment: ["error", { "beforeLineComment": true, "allowObjectStart": true }]*/

var foo = {
    // what a great and wonderful day
    day: "great"
};

const {
    // what a great and wonderful day
    foo: someDay
} = {foo: "great"};

const {
    // what a great and wonderful day
    day
} = {day: "great"};
```

选项 `{ "beforeBlockComment": true, "allowObjectStart": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint lines-around-comment: ["error", { "beforeBlockComment": true, "allowObjectStart": true }]*/

var foo = {
    /* what a great and wonderful day */
    day: "great"
};

const {
    /* what a great and wonderful day */
    foo: someDay
} = {foo: "great"};

const {
    /* what a great and wonderful day */
    day
} = {day: "great"};
```

### allowObjectEnd

选项 `{ "afterLineComment": true, "allowObjectEnd": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint lines-around-comment: ["error", { "afterLineComment": true, "allowObjectEnd": true }]*/

var foo = {
    day: "great"
    // what a great and wonderful day
};

const {
    foo: someDay
    // what a great and wonderful day
} = {foo: "great"};

const {
    day
    // what a great and wonderful day
} = {day: "great"};
```

选项 `{ "afterBlockComment": true, "allowObjectEnd": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint lines-around-comment: ["error", { "afterBlockComment": true, "allowObjectEnd": true }]*/

var foo = {
    day: "great"

    /* what a great and wonderful day */
};

const {
    foo: someDay

    /* what a great and wonderful day */
} = {foo: "great"};

const {
    day

    /* what a great and wonderful day */
} = {day: "great"};
```

### allowArrayStart

选项 `{ "beforeLineComment": true, "allowArrayStart": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint lines-around-comment: ["error", { "beforeLineComment": true, "allowArrayStart": true }]*/

var day = [
    // what a great and wonderful day
    "great",
    "wonderful"
];

const [
    // what a great and wonderful day
    someDay
] = ["great", "not great"];
```

选项 `{ "beforeBlockComment": true, "allowArrayStart": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint lines-around-comment: ["error", { "beforeBlockComment": true, "allowArrayStart": true }]*/

var day = [
    /* what a great and wonderful day */
    "great",
    "wonderful"
];

const [
    /* what a great and wonderful day */
    someDay
] = ["great", "not great"];
```

### allowArrayEnd

选项 `{ "afterLineComment": true, "allowArrayEnd": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint lines-around-comment: ["error", { "afterLineComment": true, "allowArrayEnd": true }]*/

var day = [
    "great",
    "wonderful"
    // what a great and wonderful day
];

const [
    someDay
    // what a great and wonderful day
] = ["great", "not great"];
```

选项 `{ "afterBlockComment": true, "allowArrayEnd": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint lines-around-comment: ["error", { "afterBlockComment": true, "allowArrayEnd": true }]*/

var day = [
    "great",
    "wonderful"

    /* what a great and wonderful day */
];

const [
    someDay

    /* what a great and wonderful day */
] = ["great", "not great"];
```

### ignorePattern

By default this rule ignores comments starting with the following words: `eslint`, `jshint`, `jslint`, `istanbul`, `global`, `exported`, `jscs`. To ignore more comments in addition to the defaults, set the `ignorePattern` option to a string pattern that will be passed to the [`RegExp` constructor](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/RegExp).

选项 `ignorePattern` 的 **正确** 代码示例：

::: correct

```js
/*eslint lines-around-comment: ["error"]*/

foo();
/* eslint mentioned in this comment */,
bar();

/*eslint lines-around-comment: ["error", { "ignorePattern": "pragma" }] */

foo();
/* a valid comment using pragma in it */
```

选项 `ignorePattern` 的 **错误** 代码示例：



```js
/*eslint lines-around-comment: ["error", { "ignorePattern": "pragma" }] */

1 + 1;
/* something else */
```

### applyDefaultIgnorePatterns

Default ignore patterns are applied even when `ignorePattern` is provided. If you want to omit default patterns, set this option to `false`.

选项 `{ "applyDefaultIgnorePatterns": false }` 的 **正确** 代码示例：

::: correct

```js
/*eslint lines-around-comment: ["error", { "ignorePattern": "pragma", applyDefaultIgnorePatterns: false }] */

foo();
/* a valid comment using pragma in it */
```

选项 `{ "applyDefaultIgnorePatterns": false }` 的 **错误** 代码示例：



```js
/*eslint lines-around-comment: ["error", { "applyDefaultIgnorePatterns": false }] */

foo();
/* eslint mentioned in comment */

```

## 禁用建议

Many people enjoy a terser code style and don't mind comments bumping up against code. If you fall into that category this rule is not for you.
