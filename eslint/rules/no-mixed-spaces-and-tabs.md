---
规则名: no-mixed-spaces-and-tabs
规则类型: layout
深入了解:
- https://www.emacswiki.org/emacs/SmartTabs
---



Most code conventions require either tabs or spaces be used for indentation. As such, it's usually an error if a single line of code is indented with both tabs and spaces.

## 规则详解

This rule disallows mixed spaces and tabs for indentation.

此规则的 **错误** 代码实例：



```js
/*eslint no-mixed-spaces-and-tabs: "error"*/

function add(x, y) {
// --->..return x + y;

      return x + y;
}

function main() {
// --->var x = 5,
// --->....y = 7;

    var x = 5,
        y = 7;
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-mixed-spaces-and-tabs: "error"*/

function add(x, y) {
// --->return x + y;
    return x + y;
}
```

## 配置项

This rule has a string option.

* `"smart-tabs"` allows mixed tabs and spaces when the spaces are used for alignment.

### smart-tabs

选项 `"smart-tabs"` 的 **正确** 代码示例：

::: correct

```js
/*eslint no-mixed-spaces-and-tabs: ["error", "smart-tabs"]*/

function main() {
// --->var x = 5,
// --->....y = 7;

    var x = 5,
        y = 7;
}
```
