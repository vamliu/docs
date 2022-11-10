---
规则名: no-script-url
规则类型: suggestion
深入了解:
- https://stackoverflow.com/questions/13497971/what-is-the-matter-with-script-targeted-urls
---


Using `javascript:` URLs is considered by some as a form of `eval`. Code passed in `javascript:` URLs has to be parsed and evaluated by the browser in the same way that `eval` is processed.

## 规则详解

此规则的 **错误** 代码实例：



```js
/*eslint no-script-url: "error"*/

location.href = "javascript:void(0)";

location.href = `javascript:void(0)`;
```

## 兼容

* **JSHint**: This rule corresponds to `scripturl` rule of JSHint.
