---
规则名: max-nested-callbacks
规则类型: suggestion
关联规则:
- complexity
- max-depth
- max-len
- max-lines
- max-lines-per-function
- max-params
- max-statements
深入了解:
- http://book.mixu.net/node/ch7.html
- https://web.archive.org/web/20220104141150/https://howtonode.org/control-flow
- https://web.archive.org/web/20220127215850/https://howtonode.org/control-flow-part-ii
---


Many JavaScript libraries use the callback pattern to manage asynchronous operations. A program of any complexity will most likely need to manage several asynchronous operations at various levels of concurrency. A common pitfall that is easy to fall into is nesting callbacks, which makes code more difficult to read the deeper the callbacks are nested.

```js
foo(function () {
    bar(function () {
        baz(function() {
            qux(function () {

            });
        });
    });
});
```

## 规则详解

This rule enforces a maximum depth that callbacks can be nested to increase code clarity.

## 配置项

This rule has a number or object option:

* `"max"` (default `10`) enforces a maximum depth that callbacks can be nested

**Deprecated:** The object property `maximum` is deprecated; please use the object property `max` instead.

### max

选项 `{ "max": 3 }` 的 **错误** 代码示例：



```js
/*eslint max-nested-callbacks: ["error", 3]*/

foo1(function() {
    foo2(function() {
        foo3(function() {
            foo4(function() {
                // Do something
            });
        });
    });
});
```

选项 `{ "max": 3 }` 的 **正确** 代码示例：

::: correct

```js
/*eslint max-nested-callbacks: ["error", 3]*/

foo1(handleFoo1);

function handleFoo1() {
    foo2(handleFoo2);
}

function handleFoo2() {
    foo3(handleFoo3);
}

function handleFoo3() {
    foo4(handleFoo4);
}

function handleFoo4() {
    foo5();
}
```
