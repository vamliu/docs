---
规则名: accessor-pairs
规则类型: suggestion
关联规则:
- no-dupe-keys
- no-dupe-class-members
深入了解:
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/set
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/get
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects
---

我们在写js代码时常犯的一个错误是：只为属性创建一个 setter ，而未定义相应的 getter 。由于没有 getter ，无法读取属性，所有它是不可用的。

就像这个例子：

```js
// 错误
var o = {
    set a(value) {
        this.val = value;
    }
};


// 正确
var o = {
    set a(value) {
        this.val = value;
    },
    get a() {
        return this.val;
    }
};

```
启用此规则，当定义了 setter 却没有 getter 则会触发警告，启用选项 `getWithoutSet` ，如果定义了 getter 却没有 setter 时，也会触发警告。

## 规则详解
此规则强制执行一种样式，它要求每个定义了 setter 的属性都有一个getter。

通过激活选项 `getWithoutSet` ，它强制为每个定义了 getter 的属性设置 setter 。

此规则始终检查对象字面量和属性描述。默认情况下，它还检查类声明和类表达式。

## 配置项

* `setWithoutGet` 设为 `true` 会对定义了 setter 却没有 getter 作出警告 （默认 `true`）。
* `getWithoutSet` 设为 `true` 会对定义了 getter 却没有 setter 作出警告 （默认 `false`）。
* `enforceForClassMembers` 设为 `true` 会将此规则应用于类的 getters/setters 上（默认 `true`）如果你希望此规则忽略类声明和类表达式，可将 `enforceForClassMembers` 设为 `false` 。

### setWithoutGet

默认选项 `｛"setWithoutGet"：true｝` 的 **错误** 代码示例：

```js
/*eslint accessor-pairs: "error"*/

var o = {
    set a(value) {
        this.val = value;
    }
};


var o = {d: 1};
Object.defineProperty(o, 'c', {
    set: function(value) {
        this.val = value;
    }
});
```
默认选项 `｛"setWithoutGet"：true｝` 的 **正确** 代码示例：

```js
/*eslint accessor-pairs: "error"*/

var o = {
    set a(value) {
        this.val = value;
    },
    get a() {
        return this.val;
    }
};

var o = {d: 1};
Object.defineProperty(o, 'c', {
    set: function(value) {
        this.val = value;
    },
    get: function() {
        return this.val;
    }
});

```

### getWithoutSet

选项 `｛"getWithoutSet"：true｝` 的 **错误** 代码示例：

```js
/*eslint accessor-pairs: ["error", { "getWithoutSet": true }]*/

var o = {
    set a(value) {
        this.val = value;
    }
};

var o = {
    get a() {
        return this.val;
    }
};

var o = {d: 1};
Object.defineProperty(o, 'c', {
    set: function(value) {
        this.val = value;
    }
});

var o = {d: 1};
Object.defineProperty(o, 'c', {
    get: function() {
        return this.val;
    }
});
```
选项 `{ "getWithoutSet": true }` 的 **正确** 代码示例：

```js
/*eslint accessor-pairs: ["error", { "getWithoutSet": true }]*/
var o = {
    set a(value) {
        this.val = value;
    },
    get a() {
        return this.val;
    }
};

var o = {d: 1};
Object.defineProperty(o, 'c', {
    set: function(value) {
        this.val = value;
    },
    get: function() {
        return this.val;
    }
});

```

### enforceForClassMembers

当 `enforceForClassMembers` 设置为默认值 `true` 时：

* `"getWithoutSet": true` 当类中属性定义了getters而没有setters时也会作出警告。

* `"setWithoutGet": true` 当类中属性定义了setters而没有getters时也会作出警告。

当 `enforceForClassMembers` 被设为默认值 `true` 时：


`{ "getWithoutSet": true, "enforceForClassMembers": true }` 的 **错误** 代码示例：

```js
/*eslint accessor-pairs: ["error", { "getWithoutSet": true, "enforceForClassMembers": true }]*/

class Foo {
    get a() {
        return this.val;
    }
}

class Bar {
    static get a() {
        return this.val;
    }
}

const Baz = class {
    get a() {
        return this.val;
    }
    static set a(value) {
        this.val = value;
    }
}
```

`{ "setWithoutGet": true, "enforceForClassMembers": true }` 的 **错误** 代码示例：

```js
/*eslint accessor-pairs: ["error", { "setWithoutGet": true, "enforceForClassMembers": true }]*/

class Foo {
    set a(value) {
        this.val = value;
    }
}

const Bar = class {
    static set a(value) {
        this.val = value;
    }
}
```
当 `enforceForClassMembers` 被设为 `false` 时，此规则会忽略类。

`{ "getWithoutSet": true, "setWithoutGet": true, "enforceForClassMembers": false }` 的 **正确** 代码示例：

```js
/*eslint accessor-pairs: ["error", {
    "getWithoutSet": true, "setWithoutGet": true, "enforceForClassMembers": false
}]*/

class Foo {
    get a() {
        return this.val;
    }
}

class Bar {
    static set a(value) {
        this.val = value;
    }
}

const Baz = class {
    static get a() {
        return this.val;
    }
}

const Quux = class {
    set a(value) {
        this.val = value;
    }
}
```

## 已知局限

由于静态解析的限制，此规则对通过表达式命名的属性的 getter/setter 缺失不触发警告，如以下示例所示：

```js
/*eslint accessor-pairs: "error"*/

var a = 1;

// 不触发警告
var o = {
    get [a++]() {
        return this.val;
    },
    set [a++](value) {
        this.val = value;
    }
};
```

此外，该规则不允许对象字面量和类定义中的重复键，并且在某些情况下，重复键可能不会报告getter/setter的缺失，如以下示例所示：

```js
/*eslint accessor-pairs: "error"*/

// 不触发警告
var o = {
    get a() {
        return this.val;
    },
    a: 1,
    set a(value) {
        this.val = value;
    }
};
// 上面的代码为属性“a”创建了一个只有setter的对象。
```

详见 [no-dupe-keys](no-dupe-keys) 禁用对象声明中的重复键

详见 [no-dupe-class-members](no-dupe-class-members) 禁用类声明中的重复成员变量

## 禁用建议

如果您不关心对象上是否同时存在setter和getter，可以关闭此规则。
