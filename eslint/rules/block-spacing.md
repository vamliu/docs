---
规则名: block-spacing
规则类型: layout
关联规则:
- space-before-blocks
- brace-style
---



## 规则详解

This rule enforces consistent spacing inside an open block token and the next token on the same line. This rule also enforces consistent spacing inside a close block token and previous token on the same line.

## 配置项

This rule has a string option:

* `"always"` (default) requires one or more spaces
* `"never"` disallows spaces

### always

选项 `"always"`  默认值的 **错误** 代码示例：

```js
/*eslint block-spacing: "error"*/

function foo() {return true;}
if (foo) { bar = 0;}
function baz() {let i = 0;
    return i;
}

class C {
    static {this.bar = 0;}
}
```

选项 `"always"` 默认值的 **正确** 代码示例：

```js
/*eslint block-spacing: "error"*/

function foo() { return true; }
if (foo) { bar = 0; }

class C {
    static { this.bar = 0; }
}
```

### never

选项 `"never"` 的 **错误** 代码示例：

```js
/*eslint block-spacing: ["error", "never"]*/

function foo() { return true; }
if (foo) { bar = 0;}

class C {
    static { this.bar = 0; }
}
```

选项 `"never"` 的 **正确** 代码示例：

```js
/*eslint block-spacing: ["error", "never"]*/

function foo() {return true;}
if (foo) {bar = 0;}

class C {
    static {this.bar = 0;}
}
```

## 禁用建议

If you don't want to be notified about spacing style inside of blocks, you can safely disable this rule.
