---
规则名: getter-return
规则类型: problem
深入了解:
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/get
- https://leanpub.com/understandinges6/read/#leanpub-auto-accessor-properties
---



The get syntax binds an object property to a function that will be called when that property is looked up. It was first introduced in ECMAScript 5:

```js
var p = {
    get name(){
        return "nicholas";
    }
};

Object.defineProperty(p, "age", {
    get: function (){
        return 17;
    }
});
```

Note that every `getter` is expected to return a value.

## 规则详解

This rule enforces that a return statement is present in property getters.

此规则的 **错误** 代码实例：



```js
/*eslint getter-return: "error"*/

p = {
    get name(){
        // no returns.
    }
};

Object.defineProperty(p, "age", {
    get: function (){
        // no returns.
    }
});

class P{
    get name(){
        // no returns.
    }
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint getter-return: "error"*/

p = {
    get name(){
        return "nicholas";
    }
};

Object.defineProperty(p, "age", {
    get: function (){
        return 18;
    }
});

class P{
    get name(){
        return "nicholas";
    }
}
```

## 配置项

This rule has an object option:

* `"allowImplicit": false` (default) disallows implicitly returning `undefined` with a `return` statement.

选项 `{ "allowImplicit": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint getter-return: ["error", { allowImplicit: true }]*/
p = {
    get name(){
        return; // return undefined implicitly.
    }
};
```

## 禁用建议

If your project will not be using ES5 property getters you do not need this rule.
