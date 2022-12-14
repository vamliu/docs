---
规则名: no-restricted-properties
规则类型: suggestion
关联规则:
- no-restricted-globals
- no-restricted-syntax
---


Certain properties on objects may be disallowed in a codebase. This is useful for deprecating an API or restricting usage of a module's methods. For example, you may want to disallow using `describe.only` when using Mocha or telling people to use `Object.assign` instead of `_.extend`.

## 规则详解

This rule looks for accessing a given property key on a given object name, either when reading the property's value or invoking it as a function. You may specify an optional message to indicate an alternative API or a reason for the restriction.

### 配置项

This rule takes a list of objects, where the object name and property names are specified:

```json
{
    "rules": {
        "no-restricted-properties": [2, {
            "object": "disallowedObjectName",
            "property": "disallowedPropertyName"
        }]
    }
}
```

Multiple object/property values can be disallowed, and you can specify an optional message:

```json
{
    "rules": {
        "no-restricted-properties": [2, {
            "object": "disallowedObjectName",
            "property": "disallowedPropertyName"
        }, {
            "object": "disallowedObjectName",
            "property": "anotherDisallowedPropertyName",
            "message": "Please use allowedObjectName.allowedPropertyName."
        }]
    }
}
```

If the object name is omitted, the property is disallowed for all objects:

```json
{
    "rules": {
        "no-restricted-properties": [2, {
            "property": "__defineGetter__",
            "message": "Please use Object.defineProperty instead."
        }]
    }
}
```

If the property name is omitted, accessing any property of the given object is disallowed:

```json
{
    "rules": {
        "no-restricted-properties": [2, {
            "object": "require",
            "message": "Please call require() directly."
        }]
    }
}
```

此规则的 **错误** 代码实例：



```js
/* eslint no-restricted-properties: [2, {
    "object": "disallowedObjectName",
    "property": "disallowedPropertyName"
}] */

var example = disallowedObjectName.disallowedPropertyName; /*error Disallowed object property: disallowedObjectName.disallowedPropertyName.*/

disallowedObjectName.disallowedPropertyName(); /*error Disallowed object property: disallowedObjectName.disallowedPropertyName.*/
```



```js
/* eslint no-restricted-properties: [2, {
    "property": "__defineGetter__"
}] */

foo.__defineGetter__(bar, baz);
```



```js
/* eslint no-restricted-properties: [2, {
    "object": "require"
}] */

require.resolve('foo');
```

此规则的 **正确** 代码实例：

::: correct

```js
/* eslint no-restricted-properties: [2, {
    "object": "disallowedObjectName",
    "property": "disallowedPropertyName"
}] */

var example = disallowedObjectName.somePropertyName;

allowedObjectName.disallowedPropertyName();
```

::: correct

```js
/* eslint no-restricted-properties: [2, {
    "object": "require"
}] */

require('foo');
```

## 禁用建议

If you don't have any object/property combinations to restrict, you should not use this rule.
