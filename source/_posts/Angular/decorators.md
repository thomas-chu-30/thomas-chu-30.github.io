---
tags: [angular]
title: Decorators
date: 2022-05-27 00:23:21
categories: FrontEnd
---

> Decorators 是 function 掛有 `@`前綴符號，可以用於 `class`、`paramemter`、`method` 或 `property`的前面。用來提供額外的資訊。

<!--more-->

## HostListener

@hostListener 可以監聽宿主元素上的事件，監聽 JS 的 event click | keydown | mouseleave ...

```tsx
class CountClicks {
    numberOfClicks = 0;
    // 這裡的 onClick 可以自行命名
    @HostListener("window:click", ["$event"])
    onClick(btn): void {
        console.log("button", btn, "number of clicks:", this.numberOfClicks++);
    }
}
```

## HostBinding

@HostBinding()可以為指令的宿主元素新增類、樣式、屬性等

@HostBinding()和@HostListener()不僅僅用在自定義指令，只是在自定義指令中用的較多

下面我們通過實現一個在輸入時實時改變字型和邊框顏色的指令，學習@HostBinding()和@HostListener()的用法。

```js
export class AddRainbowDirective {
    constructor() {}
    possibleColors = ["darksalmon", "hotpink", "lightskyblue", "goldenrod", "peachpuff", "mediumspringgreen", "cornflowerblue", "blanchedalmond", "lightslategrey"];
    @HostBinding("style.color") color: string;
    @HostBinding("style.borderColor") borderColor: string;
    @HostListener("keydown") onKeydown() {
        const colorPick = Math.floor(Math.random() * this.possibleColors.length);
        this.color = this.borderColor = this.possibleColors[colorPick];
    }
}
```

```html
<input appRainbow />
```

## NgModule

-   **declarations**－屬於此 NgModule 的 Component、Directive 與 Pipe 皆放置於此。
-   **imports**－此 NgModule 需要使用、依賴的其他 NgModule 皆放置於此（好像有點饒舌）。
-   **providers**－可以被整個應用程式中的任何部分被使用的 Service 皆放置於此，也可以將 Service 直接放置在 Component 的 Metadata 裡的  `providers` *（但放置在不同地方會有一些需要特別注意的事項，後續在說明 Service 時會提到。另外，在 Angular 6 之後，在 Service 之中也可以使用 Metadata 裡的  `providedIn`  宣告，該 Service 要  `provided`  到哪裡。詳細可以參考[此篇文章](https://blog.ninja-squad.com/2018/05/04/what-is-new-angular-6/)或是隔壁棚[Angular 大師之路](https://ithelp.ithome.com.tw/articles/10203876)也有提到）* 。
-   **exports**－此處放置的是，當在其他 NgModule 裡 import 了當前的 Module 後，可以在其他 NgModule 裡的 Component Template 使用的 Component、Directive 與 Pipe。
-   **entryComponents**－放在這裡的元件通常是用不通過 Route 的方式，而採用動態加入的元件。
-   **bootstrap**－在此設置的是應用程式通常稱之為 Root Component *（根元件）* ，而且只有 Root Module 才要設置此屬性。

[[功能介紹-11] NgModules - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/articles/10195338)

## Input

父層的 html

```tsx
<app-bank-account [bank]="RBC" [account-id]="4747"></app-bank-account>
```

子層的 component

```tsx
class BankAccount {
    @Input() bankName: string;
    @Input("account-id") id: string; //可以用此方把名稱改為自已想要的東西
    // TODO: 還有一個可以直接 set() 值
}
```

## Output

要使用 output 有三個步驟

1. 引入 Output & EventEmitter 的 function 在 angular
2. 讓你的 Output 有一個 EventEmitter
3. 建立一個 function 把資料 emt 上去

```tsx
import { Output, EventEmitter } from '@angular/core'; // step1

@Output() newItemEvent = new EventEmitter<string>(); // step2

addNewItem(value: string) {
    this.newItemEvent.emit(value); // step3 用這個方式 emit 資料上去
  }
}
// html <app-item (newItemEvent)="addItem($event)"></app-item>
```

## VeiwChild

抓取 DOM 也可以抓取 component 得到裡面的定義變數的值

```jsx
@ViewChild('historyBlock') historyBlock;

ngOnInit(): void {
		console.log(this.historyBlock.nativeElement) // get DOM
}
// html
<div #historyBlock> </div>
```

## VeiwChildren

用於配置檢視查詢的引數裝飾器。

```html
<ng-container *ngFor="let item of arrName">
    <hello #item [name]="item"></hello>
</ng-container>
```

```jsx
import { AfterViewInit, Component, VERSION, ViewChild } from "@angular/core";
import { HelloComponent } from "./hello.component";

@Component({
    selector: "my-app",
    templateUrl: "./app.component.html",
    styleUrls: ["./app.component.css"],
})
export class AppComponent implements AfterViewInit {
    arrName = ["aa", "bb", "cc"];
    @ViewChildren("item") itemElement: QueryList<HelloComponent>;

    ngAfterViewInit() {
        this.itemElement.map((e) => {
            console.log("itemElement", e.name); // 依序提出子組件裡的值
        });
    }
}
```

注意：`ViewChildren`  一定要搭配  `QueryList`  一起使用，不然就不能實現列表更新這件事了因生命週期關係  `ViewChild`  與  `ViewChildren`  要在  `ngAfterViewInit`  裡才能實現

## Injectable & Inject

Angular 其實提供了三種註冊 Service 的方式。

### inject 第一種

第一種方式最簡單，也是 Angular CLI 在產生 Service 時預設使用的方式：

這種方式是在 Service 自己的 Metadata 裡加上 `providedIn: 'root'` 的屬性，來告訴 Angular 說：「請把我註冊在整個系統都是使用同一個實體的注射器裡」。

```js
@Injectable({
		providedIn: 'root'
})
```

### inject 第二種

這種方式是告訴 Angular 說：「請把我註冊在這整個 NgModule 都用同一個實體的注射器裡」。也就是說，假設當初 A Service 是註冊在 A Module 裡，那麼在整個 A Module 裡就會使用同一個實體。

```js
@NgModule({
		providers: [
				BackendService,
				Logger
		],
  	...
})
```

> 那在 B Module 裡可以用 A Service 嗎？ 可以。
>
> 那在 B Module 裡的 A Service 跟在 A Module 裡的 A Service 是同一個實體嗎？同一個<心中存疑？？>

### inject 第三種

這種方式是告訴 Angular 說：「請把我註冊在這整個 Component 都用同一個實體的注射器裡」。意思是每個 Component 拿到的 Service 實體都不是同一個。

絕對不是同一個

```js
@Component({
  selector:    'app-hero-list',
  templateUrl: './hero-list.component.html',
  providers:  [ HeroService ]
})
```

這個要常常看一下，重要

https://blog.kevinyang.net/2018/01/19/angular-viewproviders-providers/

## 參考文章

[自訂 Decorators](https://blog.kevinyang.net/2017/01/30/angular2-decorators/)

[HostBinding&HostListener](https://jiaming0708.github.io/2017/03/27/angular-hostbinding-listener/)

[HostBinding&HostListener](https://jiaming0708.github.io/2017/03/27/angular-hostbinding-listener/)
