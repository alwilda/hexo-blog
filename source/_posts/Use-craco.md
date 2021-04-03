---
title: 使用 craco
date: 2021-04-03 13:22:20
tags:
categories:
---

{% blockquote gsoft-inc https://github.com/gsoft-inc/craco#craco CRACO %}
Create React App Configuration Override is an easy and comprehensible configuration layer for create-react-app.

Get all the benefits of `create-react-app` and customization without using `eject` by adding a single `craco.config.js` file at the root of your application and customize your eslint, babel, postcss configurations and many more.

All you have to do is create your app using [create-react-app](https://create-react-app.dev/) and customize the configuration with a craco.config.js file.
{% endblockquote %}

<!--more-->

# 安装

```shell
yarn add -D @craco/craco
```

创建配置文件：

```
my-app
├── node_modules
├── craco.config.js
└── package.json
```

更新脚本命令

```diff
/* package.json */

"scripts": {
-   "start": "react-scripts start",
+   "start": "craco start",
-   "build": "react-scripts build",
+   "build": "craco build"
-   "test": "react-scripts test",
+   "test": "craco test"
}
```

# 使用示例

```js
const CracoLessPlugin = require("craco-less");
const AntdDayjsWebpackPlugin = require("antd-dayjs-webpack-plugin");
const SimpleProgressWebpackPlugin = require("simple-progress-webpack-plugin");

module.exports = {
  plugins: [
    {
      plugin: CracoLessPlugin,
      options: {
        lessLoaderOptions: { lessOptions: { javascriptEnabled: true } },
      },
    },
  ],
  webpack: {
    plugins: [new AntdDayjsWebpackPlugin(), new SimpleProgressWebpackPlugin()],
  },
};
```

```json
"devDependencies": {
  "antd-dayjs-webpack-plugin": "^1.0.6",
  "craco-less": "^1.17.1",
  "simple-progress-webpack-plugin": "^1.1.2"
}
```
