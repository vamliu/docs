---
规则名: no-empty-function
布局: doc
规则类型: suggestion
关联规则:
- no-empty
---


Empty functions can reduce readability because readers need to guess whether it's intentional or not.
So writing a clear comment for empty functions is a good practice.

```js
function foo() {
    // do nothing.
}
```

Especially, the empty block of arrow functions might be confusing developers.
It's very similar to an empty object literal.

```js
list.map(() => {});   // This is a block, would return undefined.
list.map(() => ({})); // This is an empty object.
```

## 规则详解

This rule is aimed at eliminating empty functions.
A function will not be considered a problem if it contains a comment.

Examples of **incorrect** code for this rule:



```js
/*eslint no-empty-function: "error"*/
/*eslint-env es6*/

function foo() {}

var foo = function() {};

var foo = () => {};

function* foo() {}

var foo = function*() {};

var obj = {
    foo: function() {},

    foo: function*() {},

    foo() {},

    *foo() {},

    get foo() {},

    set foo(value) {}
};

class A {
    constructor() {}

    foo() {}

    *foo() {}

    get foo() {}

    set foo(value) {}

    static foo() {}

    static *foo() {}

    static get foo() {}

    static set foo(value) {}
}
```

Examples of **correct** code for this rule:

::: correct

```js
/*eslint no-empty-function: "error"*/
/*eslint-env es6*/

function foo() {
    // do nothing.
}

var foo = function() {
    // any clear comments.
};

var foo = () => {
    bar();
};

function* foo() {
    // do nothing.
}

var foo = function*() {
    // do nothing.
};

var obj = {
    foo: function() {
        // do nothing.
    },

    foo: function*() {
        // do nothing.
    },

    foo() {
        // do nothing.
    },

    *foo() {
        // do nothing.
    },

    get foo() {
        // do nothing.
    },

    set foo(value) {
        // do nothing.
    }
};

class A {
    constructor() {
        // do nothing.
    }

    foo() {
        // do nothing.
    }

    *foo() {
        // do nothing.
    }

    get foo() {
        // do nothing.
    }

    set foo(value) {
        // do nothing.
    }

    static foo() {
        // do nothing.
    }

    static *foo() {
        // do nothing.
    }

    static get foo() {
        // do nothing.
    }

    static set foo(value) {
        // do nothing.
    }
}
```

## 配置项

This rule has an option to allow specific kinds of functions to be empty.

* `allow` (`string[]`) - A list of kind to allow empty functions. List items are some of the following strings. An empty array (`[]`) by default.
    * `"functions"` - Normal functions.
    * `"arrowFunctions"` - Arrow functions.
    * `"generatorFunctions"` - Generator functions.
    * `"methods"` - Class methods and method shorthands of object literals.
    * `"generatorMethods"` - Class methods and method shorthands of object literals with generator.
    * `"getters"` - Getters.
    * `"setters"` - Setters.
    * `"constructors"` - Class constructors.
    * `"asyncFunctions"` - Async functions.
    * `"asyncMethods"` - Async class methods and method shorthands of object literals.

### allow: functions

选项 `{ "allow": ["functions"] }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-empty-function: ["error", { "allow": ["functions"] }]*/

function foo() {}

var foo = function() {};

var obj = {
    foo: function() {}
};
```

### allow: arrowFunctions

选项 `{ "allow": ["arrowFunctions"] }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-empty-function: ["error", { "allow": ["arrowFunctions"] }]*/
/*eslint-env es6*/

var foo = () => {};
```

### allow: generatorFunctions

选项 `{ "allow": ["generatorFunctions"] }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-empty-function: ["error", { "allow": ["generatorFunctions"] }]*/
/*eslint-env es6*/

function* foo() {}

var foo = function*() {};

var obj = {
    foo: function*() {}
};
```

### allow: methods

选项 `{ "allow": ["methods"] }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-empty-function: ["error", { "allow": ["methods"] }]*/
/*eslint-env es6*/

var obj = {
    foo() {}
};

class A {
    foo() {}
    static foo() {}
}
```

### allow: generatorMethods

选项 `{ "allow": ["generatorMethods"] }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-empty-function: ["error", { "allow": ["generatorMethods"] }]*/
/*eslint-env es6*/

var obj = {
    *foo() {}
};

class A {
    *foo() {}
    static *foo() {}
}
```

### allow: getters

选项 `{ "allow": ["getters"] }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-empty-function: ["error", { "allow": ["getters"] }]*/
/*eslint-env es6*/

var obj = {
    get foo() {}
};

class A {
    get foo() {}
    static get foo() {}
}
```

### allow: setters

选项 `{ "allow": ["setters"] }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-empty-function: ["error", { "allow": ["setters"] }]*/
/*eslint-env es6*/

var obj = {
    set foo(value) {}
};

class A {
    set foo(value) {}
    static set foo(value) {}
}
```

### allow: constructors

选项 `{ "allow": ["constructors"] }` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-empty-function: ["error", { "allow": ["constructors"] }]*/
/*eslint-env es6*/

class A {
    constructor() {}
}
```

### allow: asyncFunctions

Examples of **correct** code for the `{ "allow": ["asyncFunctions"] }` options:

::: correct

```js
/*eslint no-empty-function: ["error", { "allow": ["asyncFunctions"] }]*/
/*eslint-env es2017*/

async function a(){}
```

### allow: asyncMethods

Examples of **correct** code for the `{ "allow": ["asyncMethods"] }` options:

::: correct

```js
/*eslint no-empty-function: ["error", { "allow": ["asyncMethods"] }]*/
/*eslint-env es2017*/

var obj = {
    async foo() {}
};

class A {
    async foo() {}
    static async foo() {}
}
```

## 使用建议

If you don't want to be notified about empty functions, then it's safe to disable this rule.
