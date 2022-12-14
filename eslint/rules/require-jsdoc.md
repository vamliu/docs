---
规则名: require-jsdoc
规则类型: suggestion
关联规则:
- valid-jsdoc
---


This rule was [**deprecated**](https://eslint.org/blog/2018/11/jsdoc-end-of-life) in ESLint v5.10.0.

[JSDoc](http://usejsdoc.org) is a JavaScript API documentation generator. It uses specially-formatted comments inside of code to generate API documentation automatically. For example, this is what a JSDoc comment looks like for a function:

```js
/**
 * Adds two numbers together.
 * @param {int} num1 The first number.
 * @param {int} num2 The second number.
 * @returns {int} The sum of the two numbers.
 */
function sum(num1, num2) {
    return num1 + num2;
}
```

Some style guides require JSDoc comments for all functions as a way of explaining function behavior.

## 规则详解

This rule requires JSDoc comments for specified nodes. Supported nodes:

* `"FunctionDeclaration"`
* `"ClassDeclaration"`
* `"MethodDefinition"`
* `"ArrowFunctionExpression"`
* `"FunctionExpression"`

## 配置项

This rule has a single object option:

* `"require"` requires JSDoc comments for the specified nodes

Default option settings are:

```json
{
    "require-jsdoc": ["error", {
        "require": {
            "FunctionDeclaration": true,
            "MethodDefinition": false,
            "ClassDeclaration": false,
            "ArrowFunctionExpression": false,
            "FunctionExpression": false
        }
    }]
}
```

### require

选项 `{ "require": { "FunctionDeclaration": true, "MethodDefinition": true, "ClassDeclaration": true, "ArrowFunctionExpression": true, "FunctionExpression": true } }` 的 **错误** 代码示例：



```js
/*eslint "require-jsdoc": ["error", {
    "require": {
        "FunctionDeclaration": true,
        "MethodDefinition": true,
        "ClassDeclaration": true,
        "ArrowFunctionExpression": true,
        "FunctionExpression": true
    }
}]*/

function foo() {
    return 10;
}

var foo = () => {
    return 10;
};

class Foo {
    bar() {
        return 10;
    }
}

var foo = function() {
    return 10;
};

var foo = {
    bar: function() {
        return 10;
    },

    baz() {
        return 10;
    }
};
```

选项 `{ "require": { "FunctionDeclaration": true, "MethodDefinition": true, "ClassDeclaration": true, "ArrowFunctionExpression": true, "FunctionExpression": true } }` 的 **正确** 代码示例：

::: correct

```js
/*eslint "require-jsdoc": ["error", {
    "require": {
        "FunctionDeclaration": true,
        "MethodDefinition": true,
        "ClassDeclaration": true,
        "ArrowFunctionExpression": true,
        "FunctionExpression": true
    }
}]*/

/**
 * It returns 10
 */
function foo() {
    return 10;
}

/**
 * It returns test + 10
 * @params {int} test - some number
 * @returns {int} sum of test and 10
 */
var foo = (test) => {
    return test + 10;
}

/**
 * It returns 10
 */
var foo = () => {
    return 10;
}

/**
 * It returns 10
 */
var foo = function() {
    return 10;
}

var array = [1,2,3];
array.filter(function(item) {
    return item > 2;
});

/**
 * A class that can return the number 10
 */
class Foo {
    /**
    * It returns 10
    */
    bar() {
        return 10;
    }
}

/**
 * It returns 10
 */
var foo = function() {
    return 10;
};

var foo = {
    /**
    * It returns 10
    */
    bar: function() {
        return 10;
    },

    /**
    * It returns 10
    */
    baz() {
        return 10;
    }
};

setTimeout(() => {}, 10); // since it's an anonymous arrow function
```

## 禁用建议

If you do not require JSDoc for your functions, then you can leave this rule off.
