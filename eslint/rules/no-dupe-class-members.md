---
规则名: no-dupe-class-members
规则类型: problem
---



If there are declarations of the same name in class members, the last declaration overwrites other declarations silently.
It can cause unexpected behaviors.

```js
/*eslint-env es6*/

class Foo {
  bar() { console.log("hello"); }
  bar() { console.log("goodbye"); }
}

var foo = new Foo();
foo.bar(); // 正确bye
```

## 规则详解

This rule is aimed to flag the use of duplicate names in class members.

## Examples

此规则的 **错误** 代码实例：



```js
/*eslint no-dupe-class-members: "error"*/

class Foo {
  bar() { }
  bar() { }
}

class Foo {
  bar() { }
  get bar() { }
}

class Foo {
  bar;
  bar;
}

class Foo {
  bar;
  bar() { }
}

class Foo {
  static bar() { }
  static bar() { }
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-dupe-class-members: "error"*/

class Foo {
  bar() { }
  qux() { }
}

class Foo {
  get bar() { }
  set bar(value) { }
}

class Foo {
  bar;
  qux;
}

class Foo {
  bar;
  qux() { }
}

class Foo {
  static bar() { }
  bar() { }
}
```

## 禁用建议

This rule should not be used in ES3/5 environments.

In ES2015 (ES6) or later, if you don't want to be notified about duplicate names in class members, you can safely disable this rule.

It's also safe to disable this rule when using TypeScript because TypeScript's compiler already checks for duplicate function implementations.
