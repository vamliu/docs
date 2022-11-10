---
规则名: no-alert
规则类型: suggestion
关联规则:
- no-console
- no-debugger
---


JavaScript's `alert`, `confirm`, and `prompt` functions are widely considered to be obtrusive as UI elements and should be replaced by a more appropriate custom UI implementation. Furthermore, `alert` is often used while debugging code, which should be removed before deployment to production.

```js
alert("here!");
```

## 规则详解

This rule is aimed at catching debugging code that should be removed and popup UI elements that should be replaced with less obtrusive, custom UIs. As such, it will warn when it encounters `alert`, `prompt`, and `confirm` function calls which are not shadowed.

此规则的 **错误** 代码实例：

```js
/*eslint no-alert: "error"*/

alert("here!");

confirm("Are you sure?");

prompt("What's your name?", "John Doe");
```

此规则的 **正确** 代码实例：

```js
/*eslint no-alert: "error"*/

customAlert("Something happened!");

customConfirm("Are you sure?");

customPrompt("Who are you?");

function foo() {
    var alert = myCustomLib.customAlert;
    alert();
}
```
