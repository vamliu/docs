---
规则名: arrow-parens
规则类型: layout
深入了解:
- https://github.com/airbnb/javascript#arrows--one-arg-parens
---

当箭头函数只有一个参数时可以省略括号，否则，参数必须用括号括起来。此规则强制在箭头函数中统一使用括号。

## 规则详解

不管是否一致，此规则在箭头函数参数外强制使用括号。例如：

```js
/*eslint-env es6*/

// 错误
a => {}

// 正确
(a) => {}
```
遵循此样式将有助于发现进行比较（如 `>=` ）时被错误地包含在条件语句中的箭头函数（ `=>` ）。

```js
/*eslint-env es6*/

// 错误
if (a => 2) {
}

// 正确
if (a >= 2) {
}
```
该规则还可以配置成防止使用非必要的括号：

```js
/*eslint-env es6*/

// 错误
(a) => {}

// 正确
a => {}
```

## 配置项

此规则提供了一个字符串选项和一个对象选项。

字符串选项如下：

* `"always"` （默认值）强制使用括号包裹参数
* `"as-needed"` 强制只有在需要时使用括号

`"as-needed"` 选项的第二个对象参数的属性：

* `"requireForBlockBody": true` 当方法体是一个指令块（被大括号包裹的）时，需要括号。

### always

选项 `"always"`  默认值的 **错误** 代码示例：

```js
/*eslint arrow-parens: ["error", "always"]*/
/*eslint-env es6*/

a => {};
a => a;
a => {'\n'};
a.then(foo => {});
a.then(foo => a);
a(foo => { if (true) {} });
```

选项 `"always"` 默认值的 **正确** 代码示例：

```js
/*eslint arrow-parens: ["error", "always"]*/
/*eslint-env es6*/

() => {};
(a) => {};
(a) => a;
(a) => {'\n'}
a.then((foo) => {});
a.then((foo) => { if (true) {} });
```

#### If 语句

此选项有一个好处就是可以防止在条件语句中错误使用箭头函数：

```js
/*eslint-env es6*/

var a = 1;
var b = 2;
// ...
if (a => b) {
 console.log('bigger');
} else {
 console.log('smaller');
}
// 输出 'bigger', 而不是预期的 'smaller'
```
`if` 语句里的内容是一个箭头函数，而不是比较语句。

如果箭头函数是有意的，则应将其包裹在括号中以消除歧义。

```js
/*eslint-env es6*/

var a = 1;
var b = 0;
// ...
if ((a) => b) {
 console.log('truthy value returned');
} else {
 console.log('falsey value returned');
}
// 输出 'truthy value returned'
```

下面是另一个类似的例子：

```js
/*eslint-env es6*/

var a = 1, b = 2, c = 3, d = 4;
var f = a => b ? c: d;
// f = ?
```

`f` 是一个将 `a` 为参数， `b ? c: d` 为返回值的箭头函数。

它应被重写成：

```js
/*eslint-env es6*/

var a = 1, b = 2, c = 3, d = 4;
var f = (a) => b ? c: d;
```

### as-needed

选项 `"as-needed"` 的 **错误** 代码示例：

```js
/*eslint arrow-parens: ["error", "as-needed"]*/
/*eslint-env es6*/

(a) => {};
(a) => a;
(a) => {'\n'};
a.then((foo) => {});
a.then((foo) => a);
a((foo) => { if (true) {} });
const f = /** @type {number} */(a) => a + a;
const g = /* comment */ (a) => a + a;
const h = (a) /* comment */ => a + a;
```

选项 `"as-needed"` 的 **正确** 代码示例：

```js
/*eslint arrow-parens: ["error", "as-needed"]*/
/*eslint-env es6*/

() => {};
a => {};
a => a;
a => {'\n'};
a.then(foo => {});
a.then(foo => { if (true) {} });
(a, b, c) => a;
(a = 10) => a;
([a, b]) => a;
({a, b}) => a;
const f = (/** @type {number} */a) => a + a;
const g = (/* comment */ a) => a + a;
const h = (a /* comment */) => a + a;
```

### requireForBlockBody

选项 `{ "requireForBlockBody": true }` 的 **错误** 代码示例：

```js
/*eslint arrow-parens: [2, "as-needed", { "requireForBlockBody": true }]*/
/*eslint-env es6*/

(a) => a;
a => {};
a => {'\n'};
a.map((x) => x * x);
a.map(x => {
  return x * x;
});
a.then(foo => {});
```

选项 `{ "requireForBlockBody": true }` 的 **正确** 代码示例：

```js
/*eslint arrow-parens: [2, "as-needed", { "requireForBlockBody": true }]*/
/*eslint-env es6*/

(a) => {};
(a) => {'\n'};
a => ({});
() => {};
a => a;
a.then((foo) => {});
a.then((foo) => { if (true) {} });
a((foo) => { if (true) {} });
(a, b, c) => a;
(a = 10) => a;
([a, b]) => a;
({a, b}) => a;
```
