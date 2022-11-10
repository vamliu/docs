---
规则名: for-direction
规则类型: problem
---



## 规则详解

A `for` loop with a stop condition that can never be reached, such as one with a counter that moves in the wrong direction, will run infinitely. While there are occasions when an infinite loop is intended, the convention is to construct such loops as `while` loops. More typically, an infinite for loop is a bug.

此规则的 **错误** 代码实例：

```js
/*eslint for-direction: "error"*/
for (var i = 0; i < 10; i--) {
}

for (var i = 10; i >= 0; i++) {
}

for (var i = 0; i > 10; i++) {
}
```

此规则的 **正确** 代码实例：

```js
/*eslint for-direction: "error"*/
for (var i = 0; i < 10; i++) {
}
```
