---
title: 建立你的第一個 express 專案
date: 2021-07-30 23:22:41
tags:
---

# 建立專案

# 專案結構

MVC（Model–view–controller）為軟體工程中的一種軟體架構模式。它由三個部分所形成：

### **Model**

主要用來處理資料的邏輯及資料庫的部分。只要是與資料相關的事情，都會交由它處理。

### **View (api 不處理這一塊)**

將 Model 的資料透過 View 來呈現給使用者。

### **Controller**

藉由使用者的行為來控管及觸發特定的事件，並指示該事件所對應的 Model 來進行處理。

## **自定義的 Express MVC**

若使用 Express 的快速建置開發環境的專案，是還沒有做到職責分離的動作，我們可以試著將`controller`及`model`加入其中，其運作會是：

[https://viewer.diagrams.net/?border=0&highlight=0000ff&edit=\_blank&layers=1&nav=1&title=pathern-design.drawio&open=R5VnZdpswEP0aHtsDyGDnsbaTdEtPe5wmzlOPDDKolpEr5K1fXxGGPd5DzHGfzIyGEbpzdbVYQ73p6lbgmX%2FHXcI0U3dXGuprpmm0TFv9RJ517OlYZuzwBHUhKHMM6F8CTh28c%2BqSsBAoOWeSzopOhwcBcWTBh4Xgy2LYmLNirzPskYpj4GBW9T5SV%2FowCrOd%2BT8S6vlJz4Z9FbdMcRIMIwl97PJlzoWuNdQTnMv4abrqERaBl%2BDy%2BGn9yL5O7NvPP8I%2F%2BGf3y%2F23h3dxsptDXkmHIEggXzc11HKB2RzwgrHKdQKg4PPAJVESXUNdX06ZejTU428i5RoKjueSKxcX0uceDzD7yvkM4sY8kBBmRDYJ3A9RYZU9YtyZxK4byhj0oSyI7ygrlIJP0tpFCdJCRMEMjwjrYmfiPX9ojzMuVFPAAxKlchUZYCzZx11nXtWZFOth2rMyniLjvZWY%2FVW%2Bsb8Ga8%2BaQO1CPhcO2RKHYGpg4RHIR%2FXhYji6H%2BPh%2FeBh3rub3Fm%2FknzRuHL8horfEj4l6iNVgCAMS7ooTgIMc8lL4zK%2BqAegzAH0QRX6OIxGgGwmUVTApU8lGczwMyJLpTtFYuUJo8bW9RgOQ4B9BxvGikUJBTQTuZh0xk76Wq7FdjpkND64jgsiJFltRR5aW6AaiWyCucw0yEiExc%2FpT%2FLaKaXaRpxcqUIi1HDOVqoNgO5bi43Am3rDkK9Okgrmu2WqqMIv6uwLepyrFFlROcw951ROWZnIRUaicadpY0mjjhPLbVzeKZbmG2nj5s4LZVc1lBc44ZDdsAnXqq5KCjXBGSMivDj4rabBb7240lCHXD72hn1u8O2q6pAZD6nkkPyS4C8rz%2Fnhb1fgn8Yn6gtHPkX0bMh3Ksj3uxcHe1lvzg%2F7VQX2CugN3dxqNW9ST918wqvfOY3O0%2BnEa5ckzyhVNv4ueCt%2FHVRKVFm69FKieHddSfTMknQ8J5xH9UYxJ2PLU65l17EoOwk95dvOdCyCfe%2FOY5FVCzNbV6%2FFzF0Ur5uZe1yKNpSZdTPM3pNh7VoYZqPS6ncsw1pWMRGy3phhDbkSOvJ6p4mrbXtPZnbqYaZZIpR9JDPLFEfojZlZvTs5q%2FYdc1lpHMbmuplp7clM%2B39dlZWZ%2FYkah2d%2FRaPrfw%3D%3D](https://viewer.diagrams.net/?border=0&highlight=0000ff&edit=_blank&layers=1&nav=1&title=pathern-design.drawio&open=R5VnZdpswEP0aHtsDyGDnsbaTdEtPe5wmzlOPDDKolpEr5K1fXxGGPd5DzHGfzIyGEbpzdbVYQ73p6lbgmX%2FHXcI0U3dXGuprpmm0TFv9RJ517OlYZuzwBHUhKHMM6F8CTh28c%2BqSsBAoOWeSzopOhwcBcWTBh4Xgy2LYmLNirzPskYpj4GBW9T5SV%2FowCrOd%2BT8S6vlJz4Z9FbdMcRIMIwl97PJlzoWuNdQTnMv4abrqERaBl%2BDy%2BGn9yL5O7NvPP8I%2F%2BGf3y%2F23h3dxsptDXkmHIEggXzc11HKB2RzwgrHKdQKg4PPAJVESXUNdX06ZejTU428i5RoKjueSKxcX0uceDzD7yvkM4sY8kBBmRDYJ3A9RYZU9YtyZxK4byhj0oSyI7ygrlIJP0tpFCdJCRMEMjwjrYmfiPX9ojzMuVFPAAxKlchUZYCzZx11nXtWZFOth2rMyniLjvZWY%2FVW%2Bsb8Ga8%2BaQO1CPhcO2RKHYGpg4RHIR%2FXhYji6H%2BPh%2FeBh3rub3Fm%2FknzRuHL8horfEj4l6iNVgCAMS7ooTgIMc8lL4zK%2BqAegzAH0QRX6OIxGgGwmUVTApU8lGczwMyJLpTtFYuUJo8bW9RgOQ4B9BxvGikUJBTQTuZh0xk76Wq7FdjpkND64jgsiJFltRR5aW6AaiWyCucw0yEiExc%2FpT%2FLaKaXaRpxcqUIi1HDOVqoNgO5bi43Am3rDkK9Okgrmu2WqqMIv6uwLepyrFFlROcw951ROWZnIRUaicadpY0mjjhPLbVzeKZbmG2nj5s4LZVc1lBc44ZDdsAnXqq5KCjXBGSMivDj4rabBb7240lCHXD72hn1u8O2q6pAZD6nkkPyS4C8rz%2Fnhb1fgn8Yn6gtHPkX0bMh3Ksj3uxcHe1lvzg%2F7VQX2CugN3dxqNW9ST918wqvfOY3O0%2BnEa5ckzyhVNv4ueCt%2FHVRKVFm69FKieHddSfTMknQ8J5xH9UYxJ2PLU65l17EoOwk95dvOdCyCfe%2FOY5FVCzNbV6%2FFzF0Ur5uZe1yKNpSZdTPM3pNh7VoYZqPS6ncsw1pWMRGy3phhDbkSOvJ6p4mrbXtPZnbqYaZZIpR9JDPLFEfojZlZvTs5q%2FYdc1lpHMbmuplp7clM%2B39dlZWZ%2FYkah2d%2FRaPrfw%3D%3D)

![%E5%BB%BA%E7%AB%8B%E4%BD%A0%E7%9A%84%E7%AC%AC%E4%B8%80%E5%80%8B%20express%20%E5%B0%88%E6%A1%88%203db5cd7afa2c46cb948eb9d4e08e0ff1/Ib40a1T.png](%E5%BB%BA%E7%AB%8B%E4%BD%A0%E7%9A%84%E7%AC%AC%E4%B8%80%E5%80%8B%20express%20%E5%B0%88%E6%A1%88%203db5cd7afa2c46cb948eb9d4e08e0ff1/Ib40a1T.png)

資料結構就會變成：

```jsx
.
├── app.js
├── bin
│   └── www
├── controllers
│   ├── index_controller.js
├── models
│   ├── index_model.js
├── package.json
├── public
│   ├── images
│   ├── javascripts
│   └── stylesheets
│       └── style.css
├── routes
│   ├── index.js
│   └── users.js
└── views
    ├── error.ejs
    └── index.ejs
```

> vscode 打 api 套件 ⇒ [Thunder Client](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client)

## 為什麼 node 不能用 import export

模塊化編程在 js 界流行，也是基於此，隨後在瀏覽器端，requirejs 和 seajs 之類的工具包也出現了，可以說在對應規範下，require 統治了 ES6 之前的所有模塊化編程，即使現在，在 ES6 module 被完全實現之前，還是這樣。
ES6 標準發布後，module 成為標準，標準的使用是以 export 指令導出接口，以 import 引入模塊。
但因為一些歷史原因，雖然 Node.js 已經實現了 99%的 ES6 新特性，採用的卻是 CommonJS 規範，使用 require 引入模塊，使用 module.exports 導出接口。

### 什麼是 Babel

在前一篇文章中，我們談到如何安裝 Node.js 本身，本文則介紹如何安裝 Babel。

Babel 是 JavaScript 轉譯器，可將 ES6+ 程式碼轉為等效的 ES5 程式碼，我們在撰寫程式時就可以使用新的語法特性來改善程式碼的品質，而不用刻意守在舊有的手法。在實際執行 JavaScript 程式時，則會以普遍受到支援的 ES5 來執行，不用考慮 ES6 實作不夠完整的議題。

或許再過幾年，瀏覽器充份支援 ES6 的特性，那麼 Babel 專案就可以功成身退。但我們的專案並沒有白費，因為我們原本就是用 JavaScript 來寫程式，只是在版本間做了些轉換。

[node 为什么不支持 import？](https://www.html.cn/qa/node-js/10822.html)

[https://opensourcedoc.com/javascript-programming/babel/](https://opensourcedoc.com/javascript-programming/babel/)

參考文章

[Node.js-Backend 見聞錄(10)：關於後端觀念(六)-關於 MVC - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/articles/10194968)

[https://kusakawazeusu.medium.com/%E7%94%A8-typescript-%E5%AF%AB-express-route-%E8%88%87-controller-%E7%AF%87-40db4850a8f2](https://kusakawazeusu.medium.com/%E7%94%A8-typescript-%E5%AF%AB-express-route-%E8%88%87-controller-%E7%AF%87-40db4850a8f2)
