---
title: "[Angular] - Server Side Render"
date: 2022-05-27 00:23:21
tags: angular
categories: FrontEnd
---

首先把你的專案改為 ssr

```bash
ng add @nguniversal/express-engine
```

ng 會幫你新建立一些資料，資料結構如下

```bash
src/
  index.html                 app web page
  main.ts                    bootstrapper for client app
  main.server.ts             * bootstrapper for server app
  style.css                  styles for the app
  app/ ...                   application code
    app.server.module.ts     * server-side application module
server.ts                    * express web server
tsconfig.json                TypeScript base configuration
tsconfig.app.json            TypeScript browser application configuration
tsconfig.server.json         TypeScript server application configuration
tsconfig.spec.json           TypeScript tests configuration
# The files marked with * are new and not in the original tutorial sample.
```

在來啟動你的專案

```bash
npm run dev:ssr
```

透過 routerLinks 導航時能正常工作，因為它們使用的是原生的連結標籤`<a>`

## 解決 ssr 畫面閃爍問題(重要)

[[Angular Universal] 使用 TransferState 解決畫面閃爍問題 | 全端開發人員天梯](https://fullstackladder.dev/blog/2021/10/31/angular-universal-transfer-state/)
