---
规则名: no-extra-strict

深入了解:
- https://es5.github.io/#C
---

Disallows strict mode directives when already in strict mode.

(removed) This rule was **removed** in ESLint v1.0 and **replaced** by the [strict](strict) rule. The `"global"` or `"function"` options in the new rule are similar to the removed rule.

The `"use strict";` directive applies to the scope in which it appears and all inner scopes contained within that scope. Therefore, using the `"use strict";` directive in one of these inner scopes is unnecessary.

```js
"use strict";

(function () {
    "use strict";
    var foo = true;
}());
```

## 规则详解

This rule is aimed at preventing unnecessary `"use strict";` directives. As such, it will warn when it encounters a `"use strict";` directive when already in strict mode.

Example of **incorrect** code for this rule:



```js
"use strict";

(function () {
    "use strict";
    var foo = true;
}());
```

此规则的 **正确** 代码实例：

::: correct

```js
"use strict";

(function () {
    var foo = true;
}());
```

::: correct

```js
(function () {
    "use strict";
    var foo = true;
}());
```
