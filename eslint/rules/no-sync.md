---
规则名: no-sync
规则类型: suggestion
---


This rule was **deprecated** in ESLint v7.0.0. Please use the corresponding rule in [`eslint-plugin-node`](https://github.com/mysticatea/eslint-plugin-node).

In Node.js, most I/O is done through asynchronous methods. However, there are often synchronous versions of the asynchronous methods. For example, `fs.exists()` and `fs.existsSync()`. In some contexts, using synchronous operations is okay (if, as with ESLint, you are writing a command line utility). However, in other contexts the use of synchronous operations is considered a bad practice that should be avoided. For example, if you are running a high-travel web server on Node.js, you should consider carefully if you want to allow any synchronous operations that could lock up the server.

## 规则详解

This rule is aimed at preventing synchronous methods from being called in Node.js. It looks specifically for the method suffix "`Sync`" (as is the convention with Node.js operations).

## 配置项

This rule has an optional object option `{ allowAtRootLevel: <boolean> }`, which determines whether synchronous methods should be allowed at the top level of a file, outside of any functions. This option defaults to `false`.

选项 `{ allowAtRootLevel: false }`  默认值的 **错误** 代码示例：



```js
/*eslint no-sync: "error"*/

fs.existsSync(somePath);

function foo() {
  var contents = fs.readFileSync(somePath).toString();
}
```

选项 `{ allowAtRootLevel: false }` 默认值的 **正确** 代码示例：

::: correct

```js
/*eslint no-sync: "error"*/

obj.sync();

async(function() {
    // ...
});
```

Examples of **incorrect** code for this rule with the `{ allowAtRootLevel: true }` option



```js
/*eslint no-sync: ["error", { allowAtRootLevel: true }]*/

function foo() {
  var contents = fs.readFileSync(somePath).toString();
}

var bar = baz => fs.readFileSync(qux);
```

Examples of **correct** code for this rule with the `{ allowAtRootLevel: true }` option

::: correct

```js
/*eslint no-sync: ["error", { allowAtRootLevel: true }]*/

fs.readFileSync(somePath).toString();
```

## 禁用建议

If you want to allow synchronous operations in your script, do not enable this rule.
