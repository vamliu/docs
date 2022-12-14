---
规则名: default-case
规则类型: suggestion
关联规则:
- no-fallthrough
---


Some code conventions require that all `switch` statements have a `default` case, even if the default case is empty, such as:

```js
switch (foo) {
    case 1:
        doSomething();
        break;

    case 2:
        doSomething();
        break;

    default:
    // do nothing
}
```

The thinking is that it's better to always explicitly state what the default behavior should be so that it's clear whether or not the developer forgot to include the default behavior by mistake.

Other code conventions allow you to skip the `default` case so long as there is a comment indicating the omission is intentional, such as:

```js
switch (foo) {
    case 1:
        doSomething();
        break;

    case 2:
        doSomething();
        break;

    // no default
}
```

Once again, the intent here is to show that the developer intended for there to be no default behavior.

## 规则详解

This rule aims to require `default` case in `switch` statements. You may optionally include a `// no default` after the last `case` if there is no `default` case. The comment may be in any desired case, such as `// No Default`.

此规则的 **错误** 代码实例：



```js
/*eslint default-case: "error"*/

switch (a) {
    case 1:
        /* code */
        break;
}

```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint default-case: "error"*/

switch (a) {
    case 1:
        /* code */
        break;

    default:
        /* code */
        break;
}

switch (a) {
    case 1:
        /* code */
        break;

    // no default
}

switch (a) {
    case 1:
        /* code */
        break;

    // No Default
}
```

## 配置项

This rule accepts a single options argument:

* Set the `commentPattern` option to a regular expression string to change the default `/^no default$/i` comment test pattern

### commentPattern

选项 `{ "commentPattern": "^skip\\sdefault" }` 的 **正确** 代码示例：

::: correct

```js
/*eslint default-case: ["error", { "commentPattern": "^skip\\sdefault" }]*/

switch(a) {
    case 1:
        /* code */
        break;

    // skip default
}

switch(a) {
    case 1:
        /* code */
        break;

    // skip default case
}
```

## 禁用建议

If you don't want to enforce a `default` case for `switch` statements, you can safely disable this rule.
