---
规则名: func-name-matching
规则类型: suggestion
---


## 规则详解

This rule requires function names to match the name of the variable or property to which they are assigned. The rule will ignore property assignments where the property name is a literal that is not a valid identifier in the ECMAScript version specified in your configuration (default ES5).

此规则的 **错误** 代码实例：



```js
/*eslint func-name-matching: "error"*/

var foo = function bar() {};
foo = function bar() {};
obj.foo = function bar() {};
obj['foo'] = function bar() {};
var obj = {foo: function bar() {}};
({['foo']: function bar() {}});

class C {
    foo = function bar() {};
}
```



```js
/*eslint func-name-matching: ["error", "never"] */

var foo = function foo() {};
foo = function foo() {};
obj.foo = function foo() {};
obj['foo'] = function foo() {};
var obj = {foo: function foo() {}};
({['foo']: function foo() {}});

class C {
    foo = function foo() {};
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint func-name-matching: "error"*/
/*eslint func-name-matching: ["error", "always"]*/ // these are equivalent
/*eslint-env es6*/

var foo = function foo() {};
var foo = function() {};
var foo = () => {};
foo = function foo() {};

obj.foo = function foo() {};
obj['foo'] = function foo() {};
obj['foo//bar'] = function foo() {};
obj[foo] = function bar() {};

var obj = {foo: function foo() {}};
var obj = {[foo]: function bar() {}};
var obj = {'foo//bar': function foo() {}};
var obj = {foo: function() {}};

obj['x' + 2] = function bar(){};
var [ bar ] = [ function bar(){} ];
({[foo]: function bar() {}})

class C {
    foo = function foo() {};
    baz = function() {};
}

// private names are ignored
class D {
    #foo = function foo() {};
    #bar = function foo() {};
    baz() {
        this.#foo = function foo() {};
        this.#foo = function bar() {};
    }
}

module.exports = function foo(name) {};
module['exports'] = function foo(name) {};
```

::: correct

```js
/*eslint func-name-matching: ["error", "never"] */
/*eslint-env es6*/

var foo = function bar() {};
var foo = function() {};
var foo = () => {};
foo = function bar() {};

obj.foo = function bar() {};
obj['foo'] = function bar() {};
obj['foo//bar'] = function foo() {};
obj[foo] = function foo() {};

var obj = {foo: function bar() {}};
var obj = {[foo]: function foo() {}};
var obj = {'foo//bar': function foo() {}};
var obj = {foo: function() {}};

obj['x' + 2] = function bar(){};
var [ bar ] = [ function bar(){} ];
({[foo]: function bar() {}})

class C {
    foo = function bar() {};
    baz = function() {};
}

// private names are ignored
class D {
    #foo = function foo() {};
    #bar = function foo() {};
    baz() {
        this.#foo = function foo() {};
        this.#foo = function bar() {};
    }
}

module.exports = function foo(name) {};
module['exports'] = function foo(name) {};
```

## 配置项

This rule takes an optional string of "always" or "never" (when omitted, it defaults to "always"), and an optional options object with two properties `considerPropertyDescriptor` and `includeCommonJSModuleExports`.

### considerPropertyDescriptor

A boolean value that defaults to `false`. If `considerPropertyDescriptor` is set to true, the check will take into account the use of `Object.create`, `Object.defineProperty`, `Object.defineProperties`, and `Reflect.defineProperty`.

选项 `{ considerPropertyDescriptor: true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint func-name-matching: ["error", { "considerPropertyDescriptor": true }]*/
/*eslint func-name-matching: ["error", "always", { "considerPropertyDescriptor": true }]*/ // these are equivalent
var obj = {};
Object.create(obj, {foo:{value: function foo() {}}});
Object.defineProperty(obj, 'bar', {value: function bar() {}});
Object.defineProperties(obj, {baz:{value: function baz() {} }});
Reflect.defineProperty(obj, 'foo', {value: function foo() {}});
```

选项 `{ considerPropertyDescriptor: true }` 的 **错误** 代码示例：



```js
/*eslint func-name-matching: ["error", { "considerPropertyDescriptor": true }]*/
/*eslint func-name-matching: ["error", "always", { "considerPropertyDescriptor": true }]*/ // these are equivalent
var obj = {};
Object.create(obj, {foo:{value: function bar() {}}});
Object.defineProperty(obj, 'bar', {value: function baz() {}});
Object.defineProperties(obj, {baz:{value: function foo() {} }});
Reflect.defineProperty(obj, 'foo', {value: function value() {}});
```

### includeCommonJSModuleExports

A boolean value that defaults to `false`. If `includeCommonJSModuleExports` is set to true, `module.exports` and `module["exports"]` will be checked by this rule.

选项 `{ includeCommonJSModuleExports: true }` 的 **错误** 代码示例：



```js
/*eslint func-name-matching: ["error", { "includeCommonJSModuleExports": true }]*/
/*eslint func-name-matching: ["error", "always", { "includeCommonJSModuleExports": true }]*/ // these are equivalent

module.exports = function foo(name) {};
module['exports'] = function foo(name) {};
```

## 禁用建议

Do not use this rule if you want to allow named functions to have different names from the variable or property to which they are assigned.

## 兼容

* **JSCS**: [requireMatchingFunctionName](https://jscs-dev.github.io/rule/requireMatchingFunctionName)
