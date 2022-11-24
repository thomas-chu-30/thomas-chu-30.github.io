---
tags: [angular]
title: 生命週期 (Life Hooks)
date: 2022-05-27 00:23:21
categories: FrontEnd
---

![](https://ik.imagekit.io/14v7jwku5tz/Blog/%E6%88%AA%E5%9C%96_2022-10-24_%E4%B8%8B%E5%8D%8810.02.43_gU7sEkE6u.png?ik-sdk-version=javascript-1.4.3&updatedAt=1666620253816)

Angular life hoooks


### constructor

1. 初始化一些參數
2. 放外部的 `service` 引入

### ngOnInit

畫面在一開始進來的時候會執行過一次，建議在此處放 subscribe 的 function，作一些 `api` 請求動作

### ngOnChanges

當 `@Input()` 的值變化的時候，此處的就會在發生變化，執行 JS

> 注意：
>
> 如果 csr 的方式，在 default 值就會進來，input 值在進來的時候就會在進來一次。但如果是 ssr 的話，只會在 input 傳入時候才會進來

### ngDoCheck

檢測頁面上任何的變動

### ngAfterContentInit

ContentChild與ContentChildren初始化之後調用，只調用一次

### ngAfterViewInit
ViewChild與ViewChildren初始化之後調用，只調用一次

### ngAfterViewChecked

檢測，並在發生 Angular 無法或不願意自己檢測的變化時作出反應。
在每個變更檢測週期中，緊跟在 ngOnChanges() 和 ngOnInit() 後面調用,
有些特殊情況，有的時候我們需要真實的dom節點，可以再ngDoCheck判斷

### ngOnDestroy

去除 `subscribe`，銷毀事件

------

## 當數據改變的時候

第一次進來時的生命週期

1. OnChanges ⇒ 在 ngOnInit() 之前以及所繫結的一個或多個輸入屬性的值發生變化時都會呼叫。注意，如果你的元件沒有輸入，或者你使用它時沒有提供任何輸入，那麼框架就不會呼叫 ngOnChanges()。
2. OnInit ⇒ 在第一輪 ngOnChanges() 完成之後呼叫，只調用一次。
3. ngDoCheck
4. AfterContentInit
5. AfterContentChecked
6. AfterViewInit
7. AfterViewChecked

`@input`數據發生變化 (這個有一點點像是 vue 的 props)

1. ngDoCheck
2. AfterContentChecked
3. AfterViewChecked
4. OnChanges
5. DoCheck  ⇒ 意自己檢測的變化時作出反應。 欲知詳情和範例，參閱本文件中的[自訂變更檢測](https://angular.tw/guide/lifecycle-hooks#docheck)。緊跟在每次執行變更檢測時的 `ngOnChanges()` 和 首次執行變更檢測時的 `ngOnInit()` 後呼叫。
6. AfterContentChecked
7. AfterViewChecked



## Angular vs Vue


| 不同點         | Angualar                                                  | Vue                                    |
| -------------- | --------------------------------------------------------- | -------------------------------------- |
| 屬性, 方法獲得 | 任何生命週期都可以                                        | 除了 beforeCreate 生命周期，其它都可以 |
| dom 節點獲取   | 只能透過 ngDoCheck (包括 ngAfterView, ngAgteContentCheck) | Mounted 生命週期後的皆可以             |
| ngDoCheck      | 檢測頁面上的任何變動                                      | Vue 沒有類似的東西                     |
|                |                                                           |                                        |
|                |                                                           |                                        |
|                |                                                           |                                        |
|                |                                                           |                                        |

**NOTE** [angular]ngOnChange 同 [vue]update，[angular]ngOnDestory 同 [vue]destory

**參考資料**

[Angular生命周期](https://zhuanlan.zhihu.com/p/96509858)

[Angular - 生命週期鉤子](https://angular.tw/guide/lifecycle-hooks)


![Life%20Hooks%208fbaa02f1ad44ff3b76564995fcd6b7a](https://ik.imagekit.io/14v7jwku5tz/Blogger/Docusaurus/_2021-07-21_1.34.35_Dg4tjbQDl.png?ik-sdk-version=javascript-1.4.3&updatedAt=1644802619918)