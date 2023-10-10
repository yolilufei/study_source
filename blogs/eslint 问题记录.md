## extends: "eslint: recommand" 是什么意思

`extends` 是 eslint 配置中的顶级属性，用于继承其他配置文件。

#### `extends` 语法如下

`extends: string | string[]`

eslint 内部对 `eslint:recommend` 做了特殊处理: 当遇到 `eslint:recommend` 时， eslint 会将指向内置的配置文件，`eslint:all` 也是同样处理。以下是不同版本的 eslint 处理逻辑, 只是获取配置的方式有差异，本质还是一样的。

v5 
```js
if (name === "eslint:recommended") {
    /*
    * Add an explicit substitution for eslint:recommended to
    * conf/eslint-recommended.js.
    */
    return path.resolve(__dirname, "../../conf/eslint-recommended.js");
}
```
v6
```js
_loadExtendedBuiltInConfig(extendName, importerName) {
        const name = `${importerName} » ${extendName}`;

        if (extendName === "eslint:recommended") {
            return this._loadConfigData(eslintRecommendedPath, name);
        }
        if (extendName === "eslint:all") {
            return this._loadConfigData(eslintAllPath, name);
        }

        throw configMissingError(extendName, importerName);
    }
```

v7
```js
[ConfigArraySymbol.preprocessConfig](config) {
        if (config === "eslint:recommended") {
            return recommendedConfig;
        }

        if (config === "eslint:all") {
            return allConfig;
        }

        return config;
    }
```
v8
```js
if (config === "eslint:recommended") {

    // if we are in a Node.js environment warn the user
    if (typeof process !== "undefined" && process.emitWarning) {
        process.emitWarning("The 'eslint:recommended' string configuration is deprecated and will be replaced by the @eslint/js package's 'recommended' config.");
    }

    return jsPlugin.configs.recommended;
}

if (config === "eslint:all") {

    // if we are in a Node.js environment warn the user
    if (typeof process !== "undefined" && process.emitWarning) {
        process.emitWarning("The 'eslint:all' string configuration is deprecated and will be replaced by the @eslint/js package's 'all' config.");
    }

    return jsPlugin.configs.all;
}
```