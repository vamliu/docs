---
规则名: no-tabs
规则类型: layout
---


Some style guides don't allow the use of tab characters at all, including within comments.

## 规则详解

This rule looks for tabs anywhere inside a file: code, comments or anything else.

此规则的 **错误** 代码实例：



```js
var a \t= 2;

/**
* \t\t it's a test function
*/
function test(){}

var x = 1; // \t test
```

此规则的 **正确** 代码实例：

::: correct

```js
var a = 2;

/**
* it's a test function
*/
function test(){}

var x = 1; // test
```

### 配置项

This rule has an optional object option with the following properties:

* `allowIndentationTabs` (default: false): If this is set to true, then the rule will not report tabs used for indentation.

#### allowIndentationTabs

选项 `allowIndentationTabs: true` 的 **正确** 代码示例：

::: correct

```js
/* eslint no-tabs: ["error", { allowIndentationTabs: true }] */

function test() {
\tdoSomething();
}

\t// comment with leading indentation tab
```

## 禁用建议

If you have established a standard where having tabs is fine, then you can disable this rule.

## 兼容

* **JSCS**: [disallowTabs](https://jscs-dev.github.io/rule/disallowTabs)
