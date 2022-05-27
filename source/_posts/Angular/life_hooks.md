---
title: "[Angular] - Life Hooks"
date: 2022-05-27 00:23:21
tags: angular
categories: FrontEnd
---

## 生命週期

![Life%20Hooks%208fbaa02f1ad44ff3b76564995fcd6b7a/_2021-07-21_1.34.35.png](https://ik.imagekit.io/14v7jwku5tz/Blogger/Docusaurus/_2021-07-21_1.39.40_g3w-n1T7hS9.png?ik-sdk-version=javascript-1.4.3&updatedAt=1644802618366)

---

<!--more-->

### constructor

初始話一些參數

### ngOnInit

一些 api 請求

### ngOnChanges

輸入屬性的值發生改變

### ngDoCheck

檢測頁面上任何的變動

### ngAfterContentInit

ContentChild 與 ContentChildren 初始化之後調用，只調用一次

### ngAfterViewInit

ViewChild 與 ViewChildren 初始化之後調用，只調用一次

### ngAfterViewChecked

檢測，並在發生 Angular 無法或不願意自己檢測的變化時作出反應。
在每個變更檢測週期中，緊跟在 ngOnChanges() 和 ngOnInit() 後面調用,
有些特殊情況，有的時候我們需要真實的 dom 節點，可以再 ngDoCheck 判斷

### ngOnDestroy

去除訂閱，銷毀事件

---

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
5. DoCheck ⇒ 意自己檢測的變化時作出反應。 欲知詳情和範例，參閱本文件中的[自訂變更檢測](https://angular.tw/guide/lifecycle-hooks#docheck)。緊跟在每次執行變更檢測時的  `ngOnChanges()`  和 首次執行變更檢測時的  `ngOnInit()`  後呼叫。
6. AfterContentChecked
7. AfterViewChecked

## 參考資料

[Angular 生命周期](https://zhuanlan.zhihu.com/p/96509858)

[Angular - 生命週期鉤子](https://angular.tw/guide/lifecycle-hooks)

![Life%20Hooks%208fbaa02f1ad44ff3b76564995fcd6b7a](https://ik.imagekit.io/14v7jwku5tz/Blogger/Docusaurus/_2021-07-21_1.34.35_Dg4tjbQDl.png?ik-sdk-version=javascript-1.4.3&updatedAt=1644802619918)
