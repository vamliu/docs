---
规则名: array-bracket-spacing
规则类型: layout
关联规则:
- space-in-parens
- object-curly-spacing
- computed-property-spacing
---

许多样式规范都限制了数组括号和其他标记之间是否使用空格。此规则适用于数组字面量和解构赋值（ECMAScript 6）。

```js
/*eslint-env es6*/

var arr = [ 'foo', 'bar' ];
var [ x, y ] = z;

var arr = ['foo', 'bar'];
var [x,y] = z;
```

## 规则详解

此规则在数组括号内强制保持一致的间距。

## 配置项

此规则有一个字符串选项：

* `"never"` （默认值）不允许数组括号内有空格
* `"always"` 数组括号内需要至少一个空格或换行符

`"never"` 选项提供一个额外的对象配置：

* `"singleValue": true` 在只含单个元素的数组字面量的括号内需要至少一个空格或换行符
* `"objectsInArrays": true` 在数组字面量的括号和其对象括号 `[ {` 或 `} ]` 之间需要至少一个空格或换行符
* `"arraysInArrays": true` 在数组字面量的括号和其数组括号 `[ [` 或 `] ]` 之间需要至少一个空格或换行符

`"always"` 选项也提供一个额外的对象配置：

* `"singleValue": false` 在只含单个元素的数组字面量的括号内不允许空格或换行符
* `"objectsInArrays": false` 在数组字面量的括号和其对象括号 `[ {` 或 `} ]` 之间不允许空格或换行符
* `"arraysInArrays": false` 在数组字面量的括号和其数组括号 `[ [` 或 `] ]` 之间不允许空格或换行符

另外，此规则还需注意：

`"never"`（ `"always"` 也是如此）允许在数组括号内换行，因为这是一种常见的模式。

`"always"` 在空数组文本中不需要空格或换行。

### never

选项 `"never"`  默认值的 **错误** 代码示例：

```js
/*eslint array-bracket-spacing: ["error", "never"]*/
/*eslint-env es6*/

var arr = [ 'foo', 'bar' ];
var arr = ['foo', 'bar' ];
var arr = [ ['foo'], 'bar'];
var arr = [[ 'foo' ], 'bar'];
var arr = [ 'foo',
  'bar'
];
var [ x, y ] = z;
var [ x,y ] = z;
var [ x, ...y ] = z;
var [ ,,x, ] = z;
```

选项 `"never"` 默认值的 **正确** 代码示例：

```js
/*eslint array-bracket-spacing: ["error", "never"]*/
/*eslint-env es6*/

var arr = [];
var arr = ['foo', 'bar', 'baz'];
var arr = [['foo'], 'bar', 'baz'];
var arr = [
  'foo',
  'bar',
  'baz'
];
var arr = ['foo',
  'bar'
];
var arr = [
  'foo',
  'bar'];

var [x, y] = z;
var [x,y] = z;
var [x, ...y] = z;
var [,,x,] = z;
```

### always

选项 `"always"` 的 **错误** 代码示例：

```js
/*eslint array-bracket-spacing: ["error", "always"]*/
/*eslint-env es6*/

var arr = ['foo', 'bar'];
var arr = ['foo', 'bar' ];
var arr = [ ['foo'], 'bar' ];
var arr = ['foo',
  'bar'
];
var arr = [
  'foo',
  'bar'];

var [x, y] = z;
var [x,y] = z;
var [x, ...y] = z;
var [,,x,] = z;
```

选项 `"always"` 的 **正确** 代码示例：

```js
/*eslint array-bracket-spacing: ["error", "always"]*/
/*eslint-env es6*/

var arr = [];
var arr = [ 'foo', 'bar', 'baz' ];
var arr = [ [ 'foo' ], 'bar', 'baz' ];
var arr = [ 'foo',
  'bar'
];
var arr = [
  'foo',
  'bar' ];
var arr = [
  'foo',
  'bar',
  'baz'
];

var [ x, y ] = z;
var [ x,y ] = z;
var [ x, ...y ] = z;
var [ ,,x, ] = z;
```

### singleValue

选项 `"always", { "singleValue": false }`  的 **错误** 代码示例：

```js
/*eslint array-bracket-spacing: ["error", "always", { "singleValue": false }]*/

var foo = [ 'foo' ];
var foo = [ 'foo'];
var foo = ['foo' ];
var foo = [ 1 ];
var foo = [ 1];
var foo = [1 ];
var foo = [ [ 1, 2 ] ];
var foo = [ { 'foo': 'bar' } ];
```

选项 `"always", { "singleValue": false }`  的 **正确** 代码示例：

```js
/*eslint array-bracket-spacing: ["error", "always", { "singleValue": false }]*/

var foo = ['foo'];
var foo = [1];
var foo = [[ 1, 1 ]];
var foo = [{ 'foo': 'bar' }];
```

### objectsInArrays

选项 `"always", { "objectsInArrays": false }`  的 **错误** 代码示例：

```js
/*eslint array-bracket-spacing: ["error", "always", { "objectsInArrays": false }]*/

var arr = [ { 'foo': 'bar' } ];
var arr = [ {
  'foo': 'bar'
} ]
```

选项 `"always", { "objectsInArrays": false }`  的 **正确** 代码示例：

```js
/*eslint array-bracket-spacing: ["error", "always", { "objectsInArrays": false }]*/

var arr = [{ 'foo': 'bar' }];
var arr = [{
  'foo': 'bar'
}];
```

### arraysInArrays

选项 `"always", { "arraysInArrays": false }`  的 **错误** 代码示例：

```js
/*eslint array-bracket-spacing: ["error", "always", { "arraysInArrays": false }]*/

var arr = [ [ 1, 2 ], 2, 3, 4 ];
var arr = [ [ 1, 2 ], 2, [ 3, 4 ] ];
```

选项 `"always", { "arraysInArrays": false }`  的 **正确** 代码示例：

```js
/*eslint array-bracket-spacing: ["error", "always", { "arraysInArrays": false }]*/

var arr = [[ 1, 2 ], 2, 3, 4 ];
var arr = [[ 1, 2 ], 2, [ 3, 4 ]];
```

## 禁用建议

如果不需要数组括号之间间距的一致性，可以关闭此规则。
