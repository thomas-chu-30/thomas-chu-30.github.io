---
title: npm-axios [ 筆記 ]
date: 2021-08-08 13:29:48
tags: "npm"
categories: "FrontEnd"
---

## install

```
$ npm install axios
```

## 起手式

快速暴力的先使用了在說

```javascript
import axios from "axios";

axios.defaults.baseURL = [YOUR_DOMAIN];

axios.interceptors.request.use(
  (request) => {
    return request;
  },
  (error) => {
    return Promise.reject(error);
  }
);

axios.interceptors.response.use(
  (response) => {
    return response;
  },
  (error) => {
    return Promise.reject(error);
  }
);

export default axios;
```

### validateStatus

axios 會用  `validateStatus`  這個設定來決定要 resolve 或 reject 該請求的 Promise。預設當 HTTP response 的 statusCode 如下時，都會當成錯誤拋出：

```javascript
// 預設
validateStatus: function (status) {
    return status >= 200 && status < 300; // default
  },
```

## 使用 axios.create() 客製化 Axios

Axios 函式庫裡提供了  [axios.create()](https://github.com/axios/axios#creating-an-instance)  讓我們可以做客製化的設定。我們可以把需要的參數設定進來。

讓我們先來做一個設定檔，請你在 ./src/utils 資料夾中新增一支 helpers.js：

```javascript
import axios from "axios";

const baseURL = "http://example.com";

export const apiHelper = axios.create({
  baseURL,
});
```

`axios.create()`  方法會回傳一個自訂的 axios 實例，我們把它存到  `apiHelper`  變數裡，之後你會在實作中看到我們如何利用這個  `apiHelper`。

### 使用 axios.interceptors 對請求做前處理[#](https://pjchender.dev/npm/npm-axios#%E4%BD%BF%E7%94%A8-axiosinterceptors-%E5%B0%8D%E8%AB%8B%E6%B1%82%E5%81%9A%E5%89%8D%E8%99%95%E7%90%86)

透過 interceptors 的使用，可以讓 axios 在當使用者有登入（有  `token`）的情況下，把所有發出去的請求都添加上 Authorization 的標頭：

```javascript
import axios from "axios";

const baseURL = [YOUR_DOMAIN];

const axiosInstance = axios.create({
  baseURL,
});

axiosInstance.interceptors.request.use(
  (config) => {
    // 從 localStorage 將 token 取出
    const token = localStorage.getItem("token");

    // 如果 token 存在的話，則帶入到 headers 當中
    if (token) {
      config.headers["Authorization"] = `Bearer ${token}`;
    }
    return config;
  },
  (err) => Promise.reject(err)
);

export const apiHelper = axiosInstance;
```
