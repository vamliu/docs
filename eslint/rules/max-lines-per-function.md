---
规则名: max-lines-per-function
规则类型: suggestion
关联规则:
- complexity
- max-depth
- max-lines
- max-nested-callbacks
- max-params
- max-statements
- max-statements-per-line
---


Some people consider large functions a code smell. Large functions tend to do a lot of things and can make it hard following what's going on. Many coding style guides dictate a limit of the number of lines that a function can comprise of. This rule can help enforce that style.

## 规则详解

This rule enforces a maximum number of lines per function, in order to aid in maintainability and reduce complexity.

### Why not use `max-statements` or other complexity measurement rules instead?

Nested long method chains like the below example are often broken onto separate lines for readability:

```js
function() {
    return m("div", [
        m("table", {className: "table table-striped latest-data"}, [
            m("tbody",
                data.map(function(db) {
                    return m("tr", {key: db.dbname}, [
                        m("td", {className: "dbname"}, db.dbname),
                        m("td", {className: "query-count"},  [
                            m("span", {className: db.lastSample.countClassName}, db.lastSample.nbQueries)
                        ])
                    ])
                })
            )
        ])
    ])
}
```

* `max-statements` will only report this as 1 statement, despite being 16 lines of code.
* `complexity` will only report a complexity of 1
* `max-nested-callbacks` will only report 1
* `max-depth` will report a depth of 0

## 配置项

This rule has the following options that can be specified using an object:

* `"max"` (default `50`) enforces a maximum number of lines in a function.

* `"skipBlankLines"` (default `false`) ignore lines made up purely of whitespace.

* `"skipComments"` (default `false`) ignore lines containing just comments.

* `"IIFEs"` (default `false`) include any code included in IIFEs.

Alternatively, you may specify a single integer for the `max` option:

```json
"max-lines-per-function": ["error", 20]
```

is equivalent to

```json
"max-lines-per-function": ["error", { "max": 20 }]
```

### code

Examples of **incorrect** code for this rule with a max value of `2`:



```js
/*eslint max-lines-per-function: ["error", 2]*/
function foo() {
    var x = 0;
}
```



```js
/*eslint max-lines-per-function: ["error", 2]*/
function foo() {
    // a comment
    var x = 0;
}
```



```js
/*eslint max-lines-per-function: ["error", 2]*/
function foo() {
    // a comment followed by a blank line

    var x = 0;
}
```

Examples of **correct** code for this rule with a max value of `3`:

::: correct

```js
/*eslint max-lines-per-function: ["error", 3]*/
function foo() {
    var x = 0;
}
```

::: correct

```js
/*eslint max-lines-per-function: ["error", 3]*/
function foo() {
    // a comment
    var x = 0;
}
```

::: correct

```js
/*eslint max-lines-per-function: ["error", 3]*/
function foo() {
    // a comment followed by a blank line

    var x = 0;
}
```

### skipBlankLines

选项 `{ "skipBlankLines": true }` 的 **错误** 代码示例：



```js
/*eslint max-lines-per-function: ["error", {"max": 2, "skipBlankLines": true}]*/
function foo() {

    var x = 0;
}
```

选项 `{ "skipBlankLines": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint max-lines-per-function: ["error", {"max": 3, "skipBlankLines": true}]*/
function foo() {

    var x = 0;
}
```

### skipComments

选项 `{ "skipComments": true }` 的 **错误** 代码示例：



```js
/*eslint max-lines-per-function: ["error", {"max": 2, "skipComments": true}]*/
function foo() {
    // a comment
    var x = 0;
}
```

选项 `{ "skipComments": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint max-lines-per-function: ["error", {"max": 3, "skipComments": true}]*/
function foo() {
    // a comment
    var x = 0;
}
```

### IIFEs

选项 `{ "IIFEs": true }` 的 **错误** 代码示例：



```js
/*eslint max-lines-per-function: ["error", {"max": 2, "IIFEs": true}]*/
(function(){
    var x = 0;
}());

(() => {
    var x = 0;
})();
```

选项 `{ "IIFEs": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint max-lines-per-function: ["error", {"max": 3, "IIFEs": true}]*/
(function(){
    var x = 0;
}());

(() => {
    var x = 0;
})();
```

## 禁用建议

You can turn this rule off if you are not concerned with the number of lines in your functions.
