---
规则名: prefer-named-capture-group
规则类型: suggestion
关联规则:
- no-invalid-regexp
---


## 规则详解

With the landing of ECMAScript 2018, named capture groups can be used in regular expressions, which can improve their readability.
This rule is aimed at using named capture groups instead of numbered capture groups in regular expressions:

```js
const regex = /(?<year>[0-9]{4})/;
```

Alternatively, if your intention is not to _capture_ the results, but only express the alternative, use a non-capturing group:

```js
const regex = /(?:cauli|sun)flower/;
```

此规则的 **错误** 代码实例：



```js
/*eslint prefer-named-capture-group: "error"*/

const foo = /(ba[rz])/;
const bar = new RegExp('(ba[rz])');
const baz = RegExp('(ba[rz])');

foo.exec('bar')[1]; // Retrieve the group result.
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint prefer-named-capture-group: "error"*/

const foo = /(?<id>ba[rz])/;
const bar = new RegExp('(?<id>ba[rz])');
const baz = RegExp('(?<id>ba[rz])');
const xyz = /xyz(?:zy|abc)/;

foo.exec('bar').groups.id; // Retrieve the group result.
```

## 禁用建议

If you are targeting ECMAScript 2017 and/or older environments, you should not use this rule, because this ECMAScript feature is only supported in ECMAScript 2018 and/or newer environments.
