---
规则名: no-process-env
规则类型: suggestion
深入了解:
- https://stackoverflow.com/questions/5869216/how-to-store-node-js-deployment-settings-configuration-files
- https://blog.benhall.me.uk/2012/02/storing-application-config-data-in/
---


This rule was **deprecated** in ESLint v7.0.0. Please use the corresponding rule in [`eslint-plugin-node`](https://github.com/mysticatea/eslint-plugin-node).

The `process.env` object in Node.js is used to store deployment/configuration parameters. Littering it through out a project could lead to maintenance issues as it's another kind of global dependency. As such, it could lead to merge conflicts in a multi-user setup and deployment issues in a multi-server setup. Instead, one of the best practices is to define all those parameters in a single configuration/settings file which could be accessed throughout the project.

## 规则详解

This rule is aimed at discouraging use of `process.env` to avoid global dependencies. As such, it will warn whenever `process.env` is used.

此规则的 **错误** 代码实例：



```js
/*eslint no-process-env: "error"*/

if(process.env.NODE_ENV === "development") {
    //...
}
```

此规则的 **正确** 代码实例：

::: correct

```js
/*eslint no-process-env: "error"*/

var config = require("./config");

if(config.env === "development") {
    //...
}
```

## 禁用建议

If you prefer to use `process.env` throughout your project to retrieve values from environment variables, then you can safely disable this rule.
