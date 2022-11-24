---
title: Services
tags: [angular]
date: 2022-05-27 00:23:21
categories: FrontEnd
---

## **Service providers**

<!--more-->

增加一個 new service

```shell
$ ng g service [NEW_SERVICE_NAME]
```

可以看到`app.module.ts`的 providers 會增加一個名為 UserService 的類別

```typescript
providers: [UserService];
```

在使用上，如果已經有設定好 providers 後，只要在元件的 constructor 裡面宣告一個變數是 providers 裡面設定好的 service，就可以在元件裡直接取用了

```typescript
constructor(userService: UserService) {
    this.user = userService.userName;
}
```

## Service Inject

在 Angular 裡，Service 其實一個滿核心的元件，任何你在應用程式裡會需要用到的值、函式或是功能都會用到它。而它也通常是一個有著明確定義的 Class，專門用來處理某件事。

而 Angular 之所以會有 Service 這個元件是因為它想要讓我們在使用 Angular 撰寫應用時，能夠寫的更模組化一點、重用性更高一點。

所以在理想狀況下， Component 只負責處理畫面、資料綁定，而 Service 則負責像是取得資料、表單驗證等等的邏輯處理，來讓我們的應用程式擁有更好的結構與彈性。

那 Angular 是怎麼讓 Component 能夠很便利的使用 Service 呢？

答案是：**DI** (**D**ependency **I**njection，依賴注入) `@Injectable`

### **_第一種 injectable_**

使用 `@Injectable` 的話，可以在每一個 component 作引用

```typescript
@Injectable({
  providedIn: 'root'
}) // 預設的寫法
```

### **_第二種 injectable_**

這種方式是告訴 Angular 說：「請把我註冊在這整個 NgModule 都用同一個實體的注射器裡」。也就是說，假設當初 A Service 是註冊在 A Module 裡，那麼在整個 A Module 裡就會使用同一個實體。

```typescript
// src/app/app.modules.ts
@NgModule({
  providers: [
    HeroService, // 加在這裡
  ],
})
```

### **_第三種 injectable_**

註冊在 Component 裡，這種方式是告訴 Angular 說：「請把我註冊在這整個 Component 都用同一個實體的注射器裡」。意思是每個 Component 拿到的 Service 實體都不是同一個。

```typescript
@Component({
  selector:    'app-hero-list',
  templateUrl: './hero-list.component.html',
  providers:  [ HeroService ]
})
```

## 參考文章

[[Angular 深入淺出三十天] Day 17 - 基礎結構說明（四） - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/articles/10207283)

[[功能介紹-11] NgModules - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/articles/10195338)

##
