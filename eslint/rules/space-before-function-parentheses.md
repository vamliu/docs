---
规则名: space-before-function-parentheses

关联规则:
- space-after-keywords
- space-return-throw-case
---

Enforces consistent spacing before opening parenthesis in function definitions.

(removed) This rule was **removed** in ESLint v1.0 and **replaced** by the [space-before-function-paren](space-before-function-paren) rule. The name of the rule changed from "parentheses" to "paren" for consistency with the names of other rules.

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

This rule takes one argument. If it is `"always"`, which is the default option, all named functions and anonymous functions must have space before function parentheses. If `"never"` then all named functions and anonymous functions must not have space before function parentheses. If you want different spacing for named and anonymous functions you can pass a configuration object as the rule argument to configure those separately (e. g. `{"anonymous": "always", "named": "never"}`).

选项 `"always"`  默认值的 **错误** 代码示例：



```js
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
```

选项 `"always"` 默认值的 **正确** 代码示例：

::: correct

```js
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
```

选项 `"never"` 的 **错误** 代码示例：



```js
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
```

选项 `"never"` 的 **正确** 代码示例：

::: correct

```js
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
```

选项 `{"anonymous": "always", "named": "never"}` 的 **错误** 代码示例：



```js
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

选项 `{"anonymous": "always", "named": "never"}` 的 **正确** 代码示例：

::: correct

```js
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

选项 `{"anonymous": "never", "named": "always"}` 的 **错误** 代码示例：



```js
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

## 禁用建议

You can turn this rule off if you are not concerned with the consistency of spacing before function parenthesis.
