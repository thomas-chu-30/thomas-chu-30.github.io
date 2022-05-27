---
title: "[Angular] - Router"
date: 2022-05-27 00:23:21
tags: angular
categories: FrontEnd
---

## **Angular 路由**

建立 component 之後，去 `/src/app/app-routing.module.ts` 引進 component

```tsx
import { BrowserModule } from "@angular/platform-browser";
import { NgModule } from "@angular/core";
import { AppRoutingModule } from "./app-routing.module";
// CLI imports AppRoutingModule
import { AppComponent } from "./app.component";

@NgModule({
    declarations: [
        AppComponent,
        // 在這裡引入 *** components
    ],
    imports: [
        BrowserModule,
        AppRoutingModule, // CLI adds AppRoutingModule to the AppModule's imports array
    ],
    providers: [],
    bootstrap: [AppComponent],
})
export class AppModule {}
```

<!--more-->

在去 `/src/app/app-routing-modules.ts` 加上 routers

```tsx
import { NgModule } from "@angular/core";
import { Routes, RouterModule } from "@angular/router"; // CLI imports router

const routes: Routes = []; // sets up routes constant where you define your routes

// configures NgModule imports and exports
@NgModule({
    imports: [RouterModule.forRoot(routes)],
    exports: [RouterModule],
})
export class AppRoutingModule {}
```

```tsx
const routes: Routes = [
    { path: "first-component", component: FirstComponent },
    { path: "second-component", component: SecondComponent },
];

// <a routerLink="/first-component"></a>
// RouterLinkActive => 這個是用來作什麼的？？
```

## 轉址

### HTML5 URLs and the `<base href>`

The guidelines that follow will refer to different parts of a URL. This diagram outlines what those parts refer to:

```
foo://example.com:8042/over/there?name=ferret#nose
\_/   \______________/\_________/ \_________/ \__/
 |           |            |            |        |
scheme    authority      path        query   fragment
```

### template 寫法

```html
<a [routerLink]="['products']" [queryParams]="{ id: 101 }">Prodcuts</a>
<a routerLink="products" [queryParams]="{ id: 101 }">Prodcuts</a>
<a [routerLink]="['market','GP11011']">Prodcuts</a>

<!-- hash url: router_name#fragment_name -->
<a [routerLink]="['router_name']" fragment="fragment_name"></a>
```

### 用 function 轉跳網址

```tsx
import { Router } from "@angular/router";
// constructor(private router: Router){}
```

```tsx
const routes: Routes = [ { path: 'group/:id/:categories', ... }];
//
const routes: Routes = [ { path: 'group', ... }];
```

```tsx
// /market/categories/group/516/led-light
this.router.navigate(["group", 516, "led-light"]);

// group;id=7
this.router.navigate(["group", { id: 7 }]);

// group?id=7
this.router.navigate(["group"], { queryParams: { id: 7 } });

// group#prodID
this.router.navigate(["group"], { fragment: prodID });
```

[Angular Router 教學 - Wayne's Talk](https://waynestalk.com/angular-router-tutorial/)

[[功能介紹-15] Router 進階介紹 - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/articles/10195347)

[[Angular 深入淺出三十天] Day 25 - 路由總結（一） - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/articles/10209035)

### 取得參數

```tsx
export class ProductsComponent implements OnInit {
    constructor(private route: ActivatedRoute) {}
    ngOnInit() {
        // 第一種方式（較推薦）
        this.route.queryParams.subscribe((queryParams) => {
            console.log(queryParams["id"]);
        });

        // 第二種方式
        console.log(this.route.snapshot.queryParams["id"]);
    }
}
```

## 延遲 Lazy Page

在網站一開始進來的時候，不把所有網站用到的資原全部載入，由 router 對應到的 module 各別載入

### Create a feature module with routing

Next, you’ll need a feature module with a component to route to. To make one, enter the following command in the terminal, where `customers` is the name of the feature module. The path for loading the `customers` feature modules is also `customers` because it is specified with the `--route` option:

```shell
$ ng generate module customers --route customers --module app.module
```

This creates a `customers` folder having the new lazy-loadable feature module `CustomersModule` defined in the `customers.module.ts` file and the routing module `CustomersRoutingModule` defined in the `customers-routing.module.ts` file. The command automatically declares the `CustomersComponent` and imports `CustomersRoutingModule` inside the new feature module.

Because the new module is meant to be lazy-loaded, the command does NOT add a reference to the new feature module in the application's root module file, `app.module.ts`. Instead, it adds the declared route, `customers` to the `routes` array declared in the module provided as the `--module` option.

```javascript
const routes: Routes = [
    {
        path: "customers",
        loadChildren: () => import("./customers/customers.module").then((m) => m.CustomersModule),
    },
];
```

## 路由守衛

### 解決了什麼問題？

在 angular 中，路由守衛主要可以解決以下的問題

1. 對於用戶訪問頁面的權限能否進入（是否已經登錄？已經登錄的角色是否有權限？）
2. 在跳轉到組件之前獲取必須的數據 頁面時，提示用戶是否保存未提交的修改
3. 離開頁面時，提示用戶是否保存未提交的修改

Angular 幾個路由模塊提供瞭如下的接口用於幫助我們解決上面的問題

1. CanActivate 操作訪問處理系統跳轉到可以執行的地址：（判斷是否）
2. CanActivateChild 功能同 CanActivate，加點菜
3. CanDeactivate：使用處理從當前路由的情況（判斷是否存在未提交的信息）
4. CanLoad 延遲加載的方式： 是否允許通過

在經過了路由守衛，通過添加路由守衛返回的值，從而達到路由控制的最終目的

1. true：導航繼續
2. false：導航欄，用戶跳轉停留在當前的頁面或者是到指定的頁面
3. UrlTree：取消當前的導航，並導航到路由守衛返回的這個 UrlTree 上（一個新的路由信息）

### 建立一個 guard

透過 `agnular CLI` 建立一個 `guard` 來實現路由守衛，

```shell
$ ng g guard auth/auth
```

在 router 建立一個路由守衛

```javascript
const routes: Routes = [
    {
        path: "crisis-center",
        component: CrisisListComponent,
        canActivate: [AuthGuard], // 添加针对当前路由的 canActivate 路由守卫
    },
];
```

## matcher

```javascript
export const UserRoutes: Routes = [
    {
        path: "users",
        component: UserComponent,
        children: [
            {
                path: "",
                component: UserListComponent,
            },
            {
                matcher: ComplexUrlMatcher("id", /[0-9]+/),
                component: UserItemComponent,
            },
        ],
    },
];

@NgModule({
    imports: [RouterModule.forChild(UserRoutes)],
    exports: [RouterModule],
})
export class UserRoutingModule {}
```

## directive router

### [RouterLink](https://angular.io/api/router/RouterLink)

### [RouterLinkActive](https://angular.io/api/router/RouterLinkActive)

routerLinkActive 則是用來設定若現在的網址與所設定的連結一致時，要加上去的 Class 名稱，也可以利用來判斷顯示的邏輯

```javascript
<a
    routerLink="/market/categories/note"
    #rla="routerLinkActive"
    routerLinkActive="active"
>
		{{ rla.isActive ? 'isActive' : 'noActive' }} note
</a>
<a routerLink="/market/categories/book">book</a>
```

### [RouterLinkWithHref](https://angular.io/api/router/RouterLinkWithHref)

### [RouterOutlet](https://angular.io/api/router/RouterOutlet)

## 你可能會遇到的問題

---

### \*如果你重複使用 component 的話

觸發 events 的 subscribe 會經過很多的 event

[Angular](https://angular.io/api/router/Event)

[Angular 框架中去监听路由的改变（Router 中的 events: Observable ）](https://www.jianshu.com/p/de4479ce5b19)

```javascript
this.router.events.subscribe((ev) => {
    // ev 是在 event 的觸發時會跑過很多的 event
    // 這個 if 是在判斷如果 event 是 ActivationStart 的時候
    // 並且 component 同為 SupplierProductsPageComponent 時 unsubscribe
    if (ev instanceof ActivationStart && Object.is(ev?.snapshot?.component, SupplierProductsPageComponent)) {
        this.getDataSubscribe.unsubscribe();
    }
});
```

---

### 在 parent 要拿到本頁的 component

情境說明，在 header 因為要透過頁面 router 的 data 來判斷資料顯示。但在此處的 route 是直向最外面的 `app.component` ，但真正想要拿到的東西是在 firstChild 裡面，所以透過 `while` 來取得最後一個 component

```javascript
let current = this.route.firstChild;
while (current.firstChild) {
    current = current.firstChild;
}
```

> [ 注意 ] 如果是 lazy page 的話，中間會有一層 `component` 為 undefine

---

## 參考文章

[**Router 基礎介紹**](https://ithelp.ithome.com.tw/articles/10195346)

[Angular Router Tutorial](https://www.codingame.com/playgrounds/8104/angular-router-tutorial)

[Angular 使用 Router Parameters 路由參數](https://matthung0807.blogspot.com/2019/06/angular-7-router-parameters.html)

[Angular 延遲載入](https://jonny-huang.github.io/angular/training/11_angular_lazy_loading/)

[Angular 从入坑到挖坑 - 路由守卫连连看](https://www.cnblogs.com/danvic712/p/getting-started-with-angular-route-guards.html)

[詳解 Angular 中的路由守衛](https://tw511.com/a/01/26032.html)
