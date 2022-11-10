---
规则名: object-curly-newline
规则类型: layout
关联规则:
- comma-spacing
- key-spacing
- object-curly-spacing
- object-property-newline
---



A number of style guides require or disallow line breaks inside of object braces and other tokens.

## 规则详解

This rule requires or disallows a line break between `{` and its following token, and between `}` and its preceding token of object literals or destructuring assignments.

## 配置项

This rule has either a string option:

* `"always"` requires line breaks after opening and before closing braces
* `"never"` disallows line breaks after opening and before closing braces

Or an object option:

* `"multiline": true` requires line breaks if there are line breaks inside properties or between properties. Otherwise, it disallows line breaks.
* `"minProperties"` requires line breaks if the number of properties is at least the given integer. By default, an error will also be reported if an object contains linebreaks and has fewer properties than the given integer. However, the second behavior is disabled if the `consistent` option is set to `true`
* `"consistent": true` (default) requires that either both curly braces, or neither, directly enclose newlines. Note that enabling this option will also change the behavior of the `minProperties` option. (See `minProperties` above for more information)

You can specify different options for object literals, destructuring assignments, and named imports and exports:

```json
{
    "object-curly-newline": ["error", {
        "ObjectExpression": "always",
        "ObjectPattern": { "multiline": true },
        "ImportDeclaration": "never",
        "ExportDeclaration": { "multiline": true, "minProperties": 3 }
    }]
}
```

* `"ObjectExpression"` configuration for object literals
* `"ObjectPattern"` configuration for object patterns of destructuring assignments
* `"ImportDeclaration"` configuration for named imports
* `"ExportDeclaration"` configuration for named exports

### always

选项 `"always"` 的 **错误** 代码示例：



```js
/*eslint object-curly-newline: ["error", "always"]*/
/*eslint-env es6*/

let a = {};
let b = {foo: 1};
let c = {foo: 1, bar: 2};
let d = {foo: 1,
    bar: 2};
let e = {foo() {
    dosomething();
}};

let {} = obj;
let {f} = obj;
let {g, h} = obj;
let {i,
    j} = obj;
let {k = function() {
    dosomething();
}} = obj;
```

选项 `"always"` 的 **正确** 代码示例：

::: correct

```js
/*eslint object-curly-newline: ["error", "always"]*/
/*eslint-env es6*/

let a = {
};
let b = {
    foo: 1
};
let c = {
    foo: 1, bar: 2
};
let d = {
    foo: 1,
    bar: 2
};
let e = {
    foo: function() {
        dosomething();
    }
};

let {
} = obj;
let {
    f
} = obj;
let {
    g, h
} = obj;
let {
    i,
    j
} = obj;
let {
    k = function() {
        dosomething();
    }
} = obj;
```

### never

选项 `"never"` 的 **错误** 代码示例：



```js
/*eslint object-curly-newline: ["error", "never"]*/
/*eslint-env es6*/

let a = {
};
let b = {
    foo: 1
};
let c = {
    foo: 1, bar: 2
};
let d = {
    foo: 1,
    bar: 2
};
let e = {
    foo: function() {
        dosomething();
    }
};

let {
} = obj;
let {
    f
} = obj;
let {
    g, h
} = obj;
let {
    i,
    j
} = obj;
let {
    k = function() {
        dosomething();
    }
} = obj;
```

选项 `"never"` 的 **正确** 代码示例：

::: correct

```js
/*eslint object-curly-newline: ["error", "never"]*/
/*eslint-env es6*/

let a = {};
let b = {foo: 1};
let c = {foo: 1, bar: 2};
let d = {foo: 1,
    bar: 2};
let e = {foo: function() {
    dosomething();
}};

let {} = obj;
let {f} = obj;
let {g, h} = obj;
let {i,
    j} = obj;
let {k = function() {
    dosomething();
}} = obj;
```

### multiline

选项 `{ "multiline": true }` 的 **错误** 代码示例：



```js
/*eslint object-curly-newline: ["error", { "multiline": true }]*/
/*eslint-env es6*/

let a = {
};
let b = {
    foo: 1
};
let c = {
    foo: 1, bar: 2
};
let d = {foo: 1,
    bar: 2};
let e = {foo: function() {
    dosomething();
}};

let {
} = obj;
let {
    f
} = obj;
let {
    g, h
} = obj;
let {i,
    j} = obj;
let {k = function() {
    dosomething();
}} = obj;
```

选项 `{ "multiline": true }` 的 **正确** 代码示例：

::: correct

```js
/*eslint object-curly-newline: ["error", { "multiline": true }]*/
/*eslint-env es6*/

let a = {};
let b = {foo: 1};
let c = {foo: 1, bar: 2};
let d = {
    foo: 1,
    bar: 2
};
let e = {
    foo: function() {
        dosomething();
    }
};

let {} = obj;
let {f} = obj;
let {g, h} = obj;
let {
    i,
    j
} = obj;
let {
    k = function() {
        dosomething();
    }
} = obj;
```

### minProperties

选项 `{ "minProperties": 2 }` 的 **错误** 代码示例：



```js
/*eslint object-curly-newline: ["error", { "minProperties": 2 }]*/
/*eslint-env es6*/

let a = {
};
let b = {
    foo: 1
};
let c = {foo: 1, bar: 2};
let d = {foo: 1,
    bar: 2};
let e = {
    foo: function() {
        dosomething();
    }
};

let {
} = obj;
let {
    f
} = obj;
let {g, h} = obj;
let {i,
    j} = obj;
let {
    k = function() {
        dosomething();
    }
} = obj;
```

选项 `{ "minProperties": 2 }` 的 **正确** 代码示例：

::: correct

```js
/*eslint object-curly-newline: ["error", { "minProperties": 2 }]*/
/*eslint-env es6*/

let a = {};
let b = {foo: 1};
let c = {
    foo: 1, bar: 2
};
let d = {
    foo: 1,
    bar: 2
};
let e = {foo: function() {
    dosomething();
}};

let {} = obj;
let {f} = obj;
let {
    g, h
} = obj;
let {
    i,
    j
} = obj;
let {k = function() {
    dosomething();
}} = obj;
```

### consistent

选项 `{ "consistent": true }`  默认值的 **错误** 代码示例：



```js
/*eslint object-curly-newline: ["error", { "consistent": true }]*/
/*eslint-env es6*/

let a = {foo: 1
};
let b = {
    foo: 1};
let c = {foo: 1, bar: 2
};
let d = {
    foo: 1, bar: 2};
let e = {foo: function() {
    dosomething();
    }
};
let f = {
    foo: function() {
    dosomething();}};

let {g
} = obj;
let {
    h} = obj;
let {i, j
} = obj;
let {k, l
} = obj;
let {
    m, n} = obj;
let {
    o, p} = obj;
let {q = function() {
    dosomething();
    }
} = obj;
let {
    r = function() {
        dosomething();
    }} = obj;
```

选项 `{ "consistent": true }` 默认值的 **正确** 代码示例：

::: correct

```js
/*eslint object-curly-newline: ["error", { "consistent": true }]*/
/*eslint-env es6*/

let empty1 = {};
let empty2 = {
};
let a = {foo: 1};
let b = {
    foo: 1
};
let c = {
    foo: 1, bar: 2
};
let d = {
    foo: 1,
    bar: 2
};
let e = {foo: function() {dosomething();}};
let f = {
    foo: function() {
        dosomething();
    }
};

let {} = obj;
let {
} = obj;
let {g} = obj;
let {
    h
} = obj;
let {i, j} = obj;
let {
    k, l
} = obj;
let {m,
    n} = obj;
let {
    o,
    p
} = obj;
let {q = function() {dosomething();}} = obj;
let {
    r = function() {
        dosomething();
    }
} = obj;
```

### ObjectExpression and ObjectPattern

选项 `{ "ObjectExpression": "always", "ObjectPattern": "never" }`  的 **错误** 代码示例：



```js
/*eslint object-curly-newline: ["error", { "ObjectExpression": "always", "ObjectPattern": "never" }]*/
/*eslint-env es6*/

let a = {};
let b = {foo: 1};
let c = {foo: 1, bar: 2};
let d = {foo: 1,
    bar: 2};
let e = {foo: function() {
    dosomething();
}};

let {
} = obj;
let {
    f
} = obj;
let {
    g, h
} = obj;
let {
    i,
    j
} = obj;
let {
    k = function() {
        dosomething();
    }
} = obj;
```

选项 `{ "ObjectExpression": "always", "ObjectPattern": "never" }`  的 **正确** 代码示例：

::: correct

```js
/*eslint object-curly-newline: ["error", { "ObjectExpression": "always", "ObjectPattern": "never" }]*/
/*eslint-env es6*/

let a = {
};
let b = {
    foo: 1
};
let c = {
    foo: 1, bar: 2
};
let d = {
    foo: 1,
    bar: 2
};
let e = {
    foo: function() {
        dosomething();
    }
};

let {} = obj;
let {f} = obj;
let {g, h} = obj;
let {i,
    j} = obj;
let {k = function() {
    dosomething();
}} = obj;
```

### ImportDeclaration and ExportDeclaration

选项 `{ "ImportDeclaration": "always", "ExportDeclaration": "never" }`  的 **错误** 代码示例：



```js
/*eslint object-curly-newline: ["error", { "ImportDeclaration": "always", "ExportDeclaration": "never" }]*/
/*eslint-env es6*/

import {foo, bar} from 'foo-bar';
import {foo as f, bar} from 'foo-bar';
import {foo,
    bar} from 'foo-bar';

export {
   foo,
   bar
};
export {
   foo as f,
   bar
} from 'foo-bar';
```

选项 `{ "ImportDeclaration": "always", "ExportDeclaration": "never" }`  的 **正确** 代码示例：

::: correct

```js
/*eslint object-curly-newline: ["error", { "ImportDeclaration": "always", "ExportDeclaration": "never" }]*/
/*eslint-env es6*/

import {
    foo,
    bar
} from 'foo-bar';
import {
    foo, bar
} from 'foo-bar';
import {
    foo as f,
    bar
} from 'foo-bar';

export { foo, bar } from 'foo-bar';
export { foo as f, bar } from 'foo-bar';
```

## 禁用建议

If you don't want to enforce consistent line breaks after opening and before closing braces, then it's safe to disable this rule.

## 兼容

* **JSCS**: [requirePaddingNewLinesInObjects](https://jscs-dev.github.io/rule/requirePaddingNewLinesInObjects)
* **JSCS**: [disallowPaddingNewLinesInObjects](https://jscs-dev.github.io/rule/disallowPaddingNewLinesInObjects)
