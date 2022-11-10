---
规则名: arrow-body-style
规则类型: suggestion
---

箭头函数的函数体有两种语法形式。可以用 *区块* （用大括号表示） `() = > { ... }` 或单个表达式 `() => ...` 定义，其值隐式返回。

## 规则详解

此规则可以决定是否在箭头函数体外使用大括号。

## 配置项

此规则提供一个或两个选项。第一个选项为字符串，如下：

* `"always"` 强制在函数体外使用大括号
* `"as-needed"` 强制在可以省略的地方不使用大括号（默认值）
* `"never"` 强制在函数体外不使用大括号（预设每个箭头函数只返回表达式）

当第一个选项是 `"as-needed"` 时，第二个选项是一个用于更细粒度配置的对象。目前，唯一可用的选项是 `requireReturnForObjectLiteral` ，布尔属性。默认情况下为 `false` 。如果设置为 `true` ，返回值为对象时，需要大括号和显式返回。

```json
"arrow-body-style": ["error", "always"]
```

### always

选项 `"always"` 的 **错误** 代码示例：

```js
/*eslint arrow-body-style: ["error", "always"]*/
/*eslint-env es6*/
let foo = () => 0;
```

选项 `"always"` 的 **正确** 代码示例：

```js
let foo = () => {
    return 0;
};
let foo = (retv, name) => {
    retv[name] = true;
    return retv;
};
```

### as-needed

选项 `"as-needed"`  默认值的 **错误** 代码示例：

```js
/*eslint arrow-body-style: ["error", "as-needed"]*/
/*eslint-env es6*/

let foo = () => {
    return 0;
};
let foo = () => {
    return {
       bar: {
            foo: 1,
            bar: 2,
        }
    };
};
```

选项 `"as-needed"` 默认值的 **正确** 代码示例：

```js
/*eslint arrow-body-style: ["error", "as-needed"]*/
/*eslint-env es6*/

let foo = () => 0;
let foo = (retv, name) => {
    retv[name] = true;
    return retv;
};
let foo = () => ({
    bar: {
        foo: 1,
        bar: 2,
    }
});
let foo = () => { bar(); };
let foo = () => {};
let foo = () => { /* do nothing */ };
let foo = () => {
    // do nothing.
};
let foo = () => ({ bar: 0 });
```

#### requireReturnForObjectLiteral

> 此选项仅在与 `"as-needed"` 选项一起使用时适用。

选项 `{ "requireReturnForObjectLiteral": true }` 的 **错误** 代码示例：

```js
/*eslint arrow-body-style: ["error", "as-needed", { "requireReturnForObjectLiteral": true }]*/
/*eslint-env es6*/
let foo = () => ({});
let foo = () => ({ bar: 0 });
```

选项 `{ "requireReturnForObjectLiteral": true }` 的 **正确** 代码示例：

```js
/*eslint arrow-body-style: ["error", "as-needed", { "requireReturnForObjectLiteral": true }]*/
/*eslint-env es6*/

let foo = () => {};
let foo = () => { return { bar: 0 }; };
```

### never

选项 `"never"` 的 **错误** 代码示例：

```js
/*eslint arrow-body-style: ["error", "never"]*/
/*eslint-env es6*/

let foo = () => {
    return 0;
};
let foo = (retv, name) => {
    retv[name] = true;
    return retv;
};
```

选项 `"never"` 的 **正确** 代码示例：

```js
/*eslint arrow-body-style: ["error", "never"]*/
/*eslint-env es6*/

let foo = () => 0;
let foo = () => ({ foo: 0 });
```
