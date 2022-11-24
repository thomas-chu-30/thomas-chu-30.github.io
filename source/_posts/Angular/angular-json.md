---
title: Angular JSON
tags: [angular]
date: 2022-05-27 00:23:21
categories: FrontEnd
---

> 1. angular.json 是 Angular CLI 的控制塔，它提供了 Angular workspace 和 project 的預設配置。
> 2. 講解了一些 angular.json 的資料架構。
> 3. 什麼是 Architect 和 Builders 與他們之間的關係。
> 4. Angular CLI 是如何透過 Architect 解析命令的。
> 5. 如何透過 assets 在打包專案時複製完整的資料。

> Angular workspace root level 的一個文件，主要是提供 workspace 的配置與 project 的預設配置，供 Angular CLI 中 build 和 development tool 使用。
>
> A file named angular.json at the root level of an Angular workspace provides workspace-wide and project-specific configuration defaults for build and development tools provided by the Angular CLI. Path values given in the configuration are relative to the root workspace folder.

<!--more-->

## Overall JSON structure

angular.json 主要分為兩個區域： root 和 project。

### root

root 的部分主要是關於 workspace 的一些信息，主要用於配置 workspace，你會在上面找到：

-   **version**：你的 workspace 配置版本
-   **newProjectRoot**：這是用於創建新項目的路徑，比如使用 ng generate application 或 ng generate library ，那麼 Angular CLI 會藉由這個路徑知道要從哪裡生成 applicatioon 或 library。
-   **defaultProject**：這是在你使用 ng new 時所創建的屬性，他對應著你創建這個項目時給定的初始名稱，如果在使用 Angular CLI 時沒有填入項目名稱，則會直接將這個屬性帶入，比如說你要執行 app 時所使用的 ng server ，你可以直接執行 ng server 而不會出錯的原因就是它會自動將名稱帶入變成 ng server my-app。
-   **projects**：這裡包含了你的 application 和 library 所有必要的訊息。
-   **schematics**：用於客製化 ng generation 命令的預設選項。

### project

project 的部分包含 CLI 可以使用的特定訊息，你會在上面找到：

-   **root**：這是 project 相對於 workspace 的路徑。
-   **sourceroot**：這是包含當前項目 source file 的文件夾路徑。
-   **projectType**：可以是 application 或 library，CLI 需要知道專案類型，因為每種類型都有對應的需求與限制，比如說 library 需要被打包才能分發並且不能在與 application 相反的瀏覽器中提供服務。
-   **prefix**：這是當前項目 selectors 的前綴字串，當使用 ng generate component 時會將這個前綴字加在你的 component 前面，比如你的 prefix 這制為 gna，那麼使用 ng generate component hello-world 所創建出來的 component 的 selectors 就會是 "gna-hello-world"。
-   **schematics**：用於這是當前 project 中某些 schematics 所使用到的默認選項，比如你要將你專案的樣是從 CSS 變為 SCSS，就可以在這個屬性中添加 “styleext”:“scss”。
-   **architect**：為這個 project 各個 architect 提供預設值。

## What is Architect ?

可能看到這邊很多人都會覺得還可以，畢竟這些 porperty 大概都能了解在幹嘛而且也可以在自己的 Angular app 中找到對應的位置，但是！ "Architect" 這個到底是什麼？，可能對很多新手來說相當的複雜（我現在也迷迷糊糊，有說錯的話歡迎指正），接下來我們就來看看 Angular 官網是怎麼描述這個東西的。

> Architect is the tool that the CLI uses to perform complex tasks, such as compilation and test running

Architect 是 CLI 用來執行複雜任務的工具，例如 compilation 和 test running，而 Architect 是一個 shell，它根據 target configuration 執行指定的 Builder 來執行給定的任務

![](https://ithelp.ithome.com.tw/upload/images/20210729/20124767ZvVJbw5arN.png)

可以把它看作是 `Angular CLI 與 builder 之間的 "中間人"`，Architect 是可以訪問或修改特定 builder 選項或添加選項配置的地方，`當你輸入 command 後 Architect 會對 command 進行分析、解析最後對正確的 builder 執行請求操作`。

## What is Builders ?

大概了解 Architect 是什麼並且他在做什麼之後，那麼什麼是 Builders？， Builders 是 Architect 要處理特定任務時所運行的工具，通常他會對應到 npm package，例如 packageing your libreay 或 building，和 serving application。

通常 builders 會接收兩個參數，一組輸入 option ( a JSON object )，和一個 context ( a BuilderContext object )，option object 由 CLI 使用者提供，而 context 由 CLI Builder API 提供。

Angular 提供了一些由 CLI 用於 ng build 和 ng test 等命令的 builders，這些內建的 CLI Builders 可以在 angular.json 的 "Architect" 部分找到，當然你也可以當然你也可以使用 ng run 來自定你想要的 builders，不過這有點過於深入不在本章節的討論範圍。

## Understanding the command mapping

![https://ithelp.ithome.com.tw/upload/images/20210729/20124767Stj9kOMC1l.png](https://ithelp.ithome.com.tw/upload/images/20210729/20124767Stj9kOMC1l.png)

正如我們前面所說的，當你輸入 command 後 Architect 會對 command 進行分析、解析最後對正確的 builder 執行請求操作，所以當我們輸入了簡化的 command 後，實際上他會被 Architect 轉化成通用的 command : ng run projectName:architectTarget。

Example: build: ng build... → ng run :build

知道了這一點後我們可以推敲一下這些命令在 Architect 轉換後會變成什麼：

-   build: ng build … → ng run my-app:build;
-   serve: ng serve … → ng run my-app:serve;
-   e2e: ng e2e … → ng run my-app:e2e;
-   test: ng test … → ng run my-app:test;
-   lint: ng lint … → ng run my-app:lint;
-   extract-i18n: ng xi18n … → ng run my-app:xi18n

## Assets configuration

在每一個 build target 中都可以有一個陣列，裡面可以放你想要的文件或文件夾，他會在你 build 專案的時候按照原樣複製一份，不會對他進行壓縮或打包，通常會把圖片放在這邊。

```JSON
"assets": [
  "src/assets",
  "src/favicon.ico"
]
```

你可以把 Assets 的內容變為一個一個的物件，這樣相較於只有填入檔案名稱或路徑會更清楚與更清晰，將 Assets 的內容變為物件可以具有以下個 key：

-   glob：使用 node-glob 設置的基本目錄
-   input：相對於 root 目錄的路徑
-   output：相對於 outDir 的路徑，簡單來說就是 build 後存放的位置，預設是 dist / project-name
-   ignore：要排除的 glob 列表
-   followSymlinks：使否允許搜尋符號鏈接的子目錄，默認為 false

舉個例子你可以使用這些 key 更詳細描述你的 asset 路徑：

```JSON
"assets": [
  {
    "glob": "**/*",
    "input": "src/assets/",
    "output": "/assets/"
  },
  {
    "glob": "favicon.ico",
    "input": "src/",
    "output": "/"
  }
]
```

https://ithelp.ithome.com.tw/articles/10259757
