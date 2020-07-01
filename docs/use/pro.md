---
order: 4
category:
  en-US: Tutorial
  en-US: Tutorial
title:
  zh-CN: Pro 2.x
  en-US: Use in pro 2.x
---

[Ant Design pro](https://pro.ant.design) is an out-of-the-box front desk/design solution launched by Ant Design.

## file path

[Ant Design pro v2.x](https://pro.ant.design) uses umi scaffolding, the file directory is also `src/pages`, first we need to copy the downloaded Home file package directly to `pages` Under the folder.

## Modify routing

File directory: `config/router.config.js`;

Modify the route of `dashboard` and add the route of `Home`;

```js
export default [
+ {path:'/', component:'./Home' }, // Add Home route
  // user
  {
    path:'/user',
    ...
  },
  // app
  {
-path:'/',
+ path:'/dashboard', // Change the dashboard route;
    component:'../layouts/BasicLayout',
    Routes: ['src/pages/Authorized'],
    authority: ['admin','user'],
    ...
  },
];
```

## Install dependencies

For details, refer to [Installation Dependencies in Getting Started] (docs/use/getting-started#Installation Dependencies);

## CSS Modules

For multiple solutions, please check [css module used in umi](/docs/use/umi#CSS-Modules);

It is recommended to use the global of css-module;

antMotionStyle.less is as follows

```
:global {
  @import'./common.less';
  @import'./custom.less';
  @import'./content.less';
  @import'./nav0.less';
  @import'./banner0.less';
  ...
}
```

## Temporarily delete the skinning plugin

Since the skinning plugin needs to rebuild all the less, temporarily does not support landing less, so we first temporarily delete the skinning plugin.

File directory: `config/config.js`;

Delete the code related to `webpackPlugin`:
```jsx
// https://umijs.org/config/
import os from'os';
import pageRoutes from'./router.config';
-import webpackPlugin from'./plugin.config';
import defaultSettings from'../src/defaultSettings';

...

export default {
  // add for transfer to umi
  ...
  manifest: {
    basePath:'/',
  },

-chainWebpack: webpackPlugin,
};

```
