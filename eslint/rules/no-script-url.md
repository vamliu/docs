---
规则名: no-script-url
布局: doc
规则类型: suggestion
深入了解:
- https://stackoverflow.com/questions/13497971/what-is-the-matter-with-script-targeted-urls
---


Using `javascript:` URLs is considered by some as a form of `eval`. Code passed in `javascript:` URLs has to be parsed and evaluated by the browser in the same way that `eval` is processed.

## 规则详解

Examples of **incorrect** code for this rule:



```js
/*eslint no-script-url: "error"*/

location.href = "javascript:void(0)";

location.href = `javascript:void(0)`;
```

## Compatibility

* **JSHint**: This rule corresponds to `scripturl` rule of JSHint.
