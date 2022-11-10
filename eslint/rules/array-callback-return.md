---
规则名: array-callback-return
规则类型: problem
---

忘记在数组的过滤、映射和折叠方法的回调中写 `return` 语句可能会导致错误。如果你不想使用 `return` 或不需要返回的结果，请改用 [.forEach](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) 。

```js
// example: convert ['a', 'b', 'c'] --> {a: 0, b: 1, c: 2}
var indexMap = myArray.reduce(function(memo, item, index) {
  memo[item] = index;
}, {}); // Error: cannot set property 'b' of undefined
```

## 规则详解

此规则强制在数组方法的回调中使用 `return` 语句。此外，它还可以通过使用 `checkForEach` 选项强制 `forEach` 数组方法回调 **不** 返回值。

此规则检查以下方法的回调函数 `return` 语句的用法：

* [`Array.from`](https://www.ecma-international.org/ecma-262/6.0/#sec-array.from)
* [`Array.prototype.every`](https://www.ecma-international.org/ecma-262/6.0/#sec-array.prototype.every)
* [`Array.prototype.filter`](https://www.ecma-international.org/ecma-262/6.0/#sec-array.prototype.filter)
* [`Array.prototype.find`](https://www.ecma-international.org/ecma-262/6.0/#sec-array.prototype.find)
* [`Array.prototype.findIndex`](https://www.ecma-international.org/ecma-262/6.0/#sec-array.prototype.findindex)
* [`Array.prototype.findLast`](https://tc39.es/ecma262/#sec-array.prototype.findlast)
* [`Array.prototype.findLastIndex`](https://tc39.es/ecma262/#sec-array.prototype.findlastindex)
* [`Array.prototype.flatMap`](https://www.ecma-international.org/ecma-262/10.0/#sec-array.prototype.flatmap)
* [`Array.prototype.forEach`](https://www.ecma-international.org/ecma-262/6.0/#sec-array.prototype.foreach) (可选，基于 `checkForEach` 参数)
* [`Array.prototype.map`](https://www.ecma-international.org/ecma-262/6.0/#sec-array.prototype.map)
* [`Array.prototype.reduce`](https://www.ecma-international.org/ecma-262/6.0/#sec-array.prototype.reduce)
* [`Array.prototype.reduceRight`](https://www.ecma-international.org/ecma-262/6.0/#sec-array.prototype.reduceright)
* [`Array.prototype.some`](https://www.ecma-international.org/ecma-262/6.0/#sec-array.prototype.some)
* [`Array.prototype.sort`](https://www.ecma-international.org/ecma-262/6.0/#sec-array.prototype.sort)
* 以及数组实例的以上类型方法。

此规则的 **错误** 代码实例：

```js
/*eslint array-callback-return: "error"*/

var indexMap = myArray.reduce(function(memo, item, index) {
    memo[item] = index;
}, {});

var foo = Array.from(nodes, function(node) {
    if (node.tagName === "DIV") {
        return true;
    }
});

var bar = foo.filter(function(x) {
    if (x) {
        return true;
    } else {
        return;
    }
});
```

此规则的 **正确** 代码实例：

```js
/*eslint array-callback-return: "error"*/

var indexMap = myArray.reduce(function(memo, item, index) {
    memo[item] = index;
    return memo;
}, {});

var foo = Array.from(nodes, function(node) {
    if (node.tagName === "DIV") {
        return true;
    }
    return false;
});

var bar = foo.map(node => node.getAttribute("id"));
```

## 配置项

此规则接受两个选项的配置对象：

* `"allowImplicit": false` （默认值）当设置为 `true` 时，允许需要返回值的方法回调 `return` 语句隐式返回不包含表达式的 `undefined` 。
* `"checkForEach": false` （默认）设置为true时，规则将会应用于 `forEach` 的回调。

### allowImplicit

选项 `{ "allowImplicit": true }` 的 **正确** 代码示例：

```js
/*eslint array-callback-return: ["error", { allowImplicit: true }]*/
var undefAllTheThings = myArray.map(function(item) {
    return;
});
```

### checkForEach

选项 `{ "checkForEach": true }` 的 **错误** 代码示例：

```js
/*eslint array-callback-return: ["error", { checkForEach: true }]*/

myArray.forEach(function(item) {
    return handleItem(item)
});

myArray.forEach(function(item) {
    if (item < 0) {
        return x;
    }
    handleItem(item);
});

myArray.forEach(item => handleItem(item));

myArray.forEach(item => {
    return handleItem(item);
});
```

选项 `{ "checkForEach": true }` 的 **正确** 代码示例：

```js
/*eslint array-callback-return: ["error", { checkForEach: true }]*/

myArray.forEach(function(item) {
    handleItem(item)
});

myArray.forEach(function(item) {
    if (item < 0) {
        return;
    }
    handleItem(item);
});

myArray.forEach(function(item) {
    handleItem(item);
    return;
});

myArray.forEach(item => {
    handleItem(item);
});
```

## 已知局限

此规则匹配给定方法名称，即使拥有该方法的对象类型 *不* 是数组，也会检查该方法的回调函数。

## 禁用建议

如果您不想在数组方法的回调中使用 `return` 语句触发警告，那么禁用此规则是安全的。
