---
规则名: space-before-function-paren
规则类型: layout
关联规则:
- space-after-keywords
- space-return-throw-case
---



When formatting a function, whitespace is allowed between the function name or `function` keyword and the opening paren. Named functions also require a space between the `function` keyword and the function name, but anonymous functions require no whitespace. For example:

```js
function withoutSpace(x) {
    // ...
}

function withSpace (x) {
    // ...
}

var anonymousWithoutSpace = function() {};

var anonymousWithSpace = function () {};
```

Style guides may require a space after the `function` keyword for anonymous functions, while others specify no whitespace. Similarly, the space after a function name may or may not be required.

## 规则详解

This rule aims to enforce consistent spacing before function parentheses and as such, will warn whenever whitespace doesn't match the preferences specified.

## 配置项

This rule has a string option or an object option:

```js
{
    "space-before-function-paren": ["error", "always"],
    // or
    "space-before-function-paren": ["error", {
        "anonymous": "always",
        "named": "always",
        "asyncArrow": "always"
    }],
}
```

* `always` (default) requires a space followed by the `(` of arguments.
* `never` disallows any space followed by the `(` of arguments.

The string option does not check async arrow function expressions for backward compatibility.

You can also use a separate option for each type of function.
Each of the following options can be set to `"always"`, `"never"`, or `"ignore"`. The default is `"always"`.

* `anonymous` is for anonymous function expressions (e.g. `function () {}`).
* `named` is for named function expressions (e.g. `function foo () {}`).
* `asyncArrow` is for async arrow function expressions (e.g. `async () => {}`).

### "always"

选项 `"always"`  默认值的 **错误** 代码示例：



```js
/*eslint space-before-function-paren: "error"*/
/*eslint-env es6*/

function foo() {
    // ...
}

var bar = function() {
    // ...
};

var bar = function foo() {
    // ...
};

class Foo {
    constructor() {
        // ...
    }
}

var foo = {
    bar() {
        // ...
    }
};

var foo = async() => 1
```

选项 `"always"` 默认值的 **正确** 代码示例：

::: correct

```js
/*eslint space-before-function-paren: "error"*/
/*eslint-env es6*/

function foo () {
    // ...
}

var bar = function () {
    // ...
};

var bar = function foo () {
    // ...
};

class Foo {
    constructor () {
        // ...
    }
}

var foo = {
    bar () {
        // ...
    }
};

var foo = async () => 1
```

### "never"

选项 `"never"` 的 **错误** 代码示例：



```js
/*eslint space-before-function-paren: ["error", "never"]*/
/*eslint-env es6*/

function foo () {
    // ...
}

var bar = function () {
    // ...
};

var bar = function foo () {
    // ...
};

class Foo {
    constructor () {
        // ...
    }
}

var foo = {
    bar () {
        // ...
    }
};

var foo = async () => 1
```

选项 `"never"` 的 **正确** 代码示例：

::: correct

```js
/*eslint space-before-function-paren: ["error", "never"]*/
/*eslint-env es6*/

function foo() {
    // ...
}

var bar = function() {
    // ...
};

var bar = function foo() {
    // ...
};

class Foo {
    constructor() {
        // ...
    }
}

var foo = {
    bar() {
        // ...
    }
};

var foo = async() => 1
```

### `{"anonymous": "always", "named": "never", "asyncArrow": "always"}`

选项 `{"anonymous": "always", "named": "never", "asyncArrow": "always"}` 的 **错误** 代码示例：



```js
/*eslint space-before-function-paren: ["error", {"anonymous": "always", "named": "never", "asyncArrow": "always"}]*/
/*eslint-env es6*/

function foo () {
    // ...
}

var bar = function() {
    // ...
};

class Foo {
    constructor () {
        // ...
    }
}

var foo = {
    bar () {
        // ...
    }
};

var foo = async(a) => await a
```

选项 `{"anonymous": "always", "named": "never", "asyncArrow": "always"}` 的 **正确** 代码示例：

::: correct

```js
/*eslint space-before-function-paren: ["error", {"anonymous": "always", "named": "never", "asyncArrow": "always"}]*/
/*eslint-env es6*/

function foo() {
    // ...
}

var bar = function () {
    // ...
};

class Foo {
    constructor() {
        // ...
    }
}

var foo = {
    bar() {
        // ...
    }
};

var foo = async (a) => await a
```

### `{"anonymous": "never", "named": "always"}`

选项 `{"anonymous": "never", "named": "always"}` 的 **错误** 代码示例：



```js
/*eslint space-before-function-paren: ["error", { "anonymous": "never", "named": "always" }]*/
/*eslint-env es6*/

function foo() {
    // ...
}

var bar = function () {
    // ...
};

class Foo {
    constructor() {
        // ...
    }
}

var foo = {
    bar() {
        // ...
    }
};
```

选项 `{"anonymous": "never", "named": "always"}` 的 **正确** 代码示例：

::: correct

```js
/*eslint space-before-function-paren: ["error", { "anonymous": "never", "named": "always" }]*/
/*eslint-env es6*/

function foo () {
    // ...
}

var bar = function() {
    // ...
};

class Foo {
    constructor () {
        // ...
    }
}

var foo = {
    bar () {
        // ...
    }
};
```

### `{"anonymous": "ignore", "named": "always"}`

选项 `{"anonymous": "ignore", "named": "always"}` 的 **错误** 代码示例：



```js
/*eslint space-before-function-paren: ["error", { "anonymous": "ignore", "named": "always" }]*/
/*eslint-env es6*/

function foo() {
    // ...
}

class Foo {
    constructor() {
        // ...
    }
}

var foo = {
    bar() {
        // ...
    }
};
```

选项 `{"anonymous": "ignore", "named": "always"}` 的 **正确** 代码示例：

::: correct

```js
/*eslint space-before-function-paren: ["error", { "anonymous": "ignore", "named": "always" }]*/
/*eslint-env es6*/

var bar = function() {
    // ...
};

var bar = function () {
    // ...
};

function foo () {
    // ...
}

class Foo {
    constructor () {
        // ...
    }
}

var foo = {
    bar () {
        // ...
    }
};
```

## 禁用建议

You can turn this rule off if you are not concerned with the consistency of spacing before function parenthesis.
