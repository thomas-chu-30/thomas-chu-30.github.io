---
tags: [angular]
title: Directive
date: 2022-05-27 00:23:21
categories: FrontEnd
---



## Commom (11)

## class style bind

```html
<!-- Native Class and Style Attributes -->
<input class="is-danger my-button" style="border: none; color: blue" />

<!-- Angular class and style Bindings -->
<input [class.is-danger]="booleanProp" [style.border]="borderProp" />

<!-- ngClass -->
<input [ngClass]="{'is-danger': booleanProp, 'myButton': true}" />
<input [ngClass]="isDangerButton" />

<!-- ngStyle -->
<input [ngStyle]="{'border': borderProp, 'color': colorProp}" />
<input [ngStyle]="hasColorBorder" />
```

[精通 Angular 之 NgClass 和 NgStyle](https://zhuanlan.zhihu.com/p/95490706)

[angularJs 中关于 ng-class 的三种使用方式说明](https://segmentfault.com/a/1190000008393758)

[Angular - Attribute 繫結、類別繫結和樣式繫結](https://angular.tw/guide/attribute-binding)

## ngFor

```js
*ngFor="
  let item of items;
  let idx = index;
  let first = first;
  let last = last;
  let even = even;
  let odd = odd"
```

使用 NgFor 時，我們可以同時搭配使用五個不同的變數，分別是：

-   index：整數值；代表目前資料在陣列中的 index
-   first：布林值；代表目前資料是否為 第一筆
-   last：布林值；代表目前資料是否為 最後一筆
-   even：布林值；代表目前資料的 index 是否為 第偶數筆
-   odd：布林值；代表目前資料的 index 是否為 第奇數筆

[全端開發人員天梯](https://dotblogs.com.tw/wellwind/2017/01/01/angular2-ngfor-vars)

## ngIf

> ngIf 會直接看 DOM 不見，而 `[hidden]` 的這個寫法只會讓 dom 看不見

```html
<div *ngIf="false">test</div>
<div [hidden]="true">
<!- [style.display]="!isLoading ? 'block' : 'none'" ->
```

`ngIf` `else` 的 組合技

```html
<div *ngIf="display; else anotherWord">Hello</div>
<ng-template #anotherWord>
  <div>World</div>
</ng-template>
<button (click)="display = !display">Toggle Display</button>
```



## [(ngModel)]

> 一定要引用 `import { FormsModule } from '@angular/forms';` > `imports: [FormsModule]`
> 不然會沒有辦法使用

有三種寫法都可以達到雙向綁定的效果

### 綁定方法1

使用 `[()]` 的寫法

```html
<input [(ngModel)]="username">

<p>Hello {{username}}!</p>
```

### 綁定方法2

將 `[]` `()` 分開寫

```html
<input [ngModel]="username" (ngModelChange)="username = $event">

<p>Hello {{username}}!</p>
```

### 綁定方法3

不使用 `ngModel`

```html
<input [value]="username" (input)="username = $event.target.value">

<p>Hello {{username}}!</p>
```

[ngMode 底層說明l](https://blog.kevinyang.net/2017/08/14/angular-two-way-binding/)

[[Angular 深入淺出三十天] Day 09 - Angular 小學堂（二） - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/articles/10205162)

## NgTemplateOutLet

[](https://www.tektutorialshub.com/angular/ngtemplateoutlet-in-angular/)

## NgPlural

## NgPluraCase

```html
<some-element [ngPlural]="value">
    <ng-template ngPluralCase="=0">there is nothing</ng-template>
    <ng-template ngPluralCase="=1">there is one</ng-template>
    <ng-template ngPluralCase="few">there are a few</ng-template>
</some-element>
```

## NgSwitch

## NgSwitchCase

## **NgSwitchDefault**

```html
// homepage.component.html

<ng-container *ngFor="let link of links">
    <div [ngSwitch]="link?.name">
        <div *ngSwitchCase="'HOME'" style="color: blue">{{link?.name}}</div>
        <div *ngSwitchCase="'ABOUT US'" style="color:red">{{link?.name}}</div>
        <div *ngSwitchCase="'Students'" style="color: green">{{link?.name}}</div>
        <div *ngSwitchCase="'Teachers'" style="color:violet">{{link?.name}}</div>
        <div *ngSwitchDefault>output2</div>
    </div>
</ng-container>
```

## Forms (27)

## Router (4)

[參考 router page](/docs/Angular-Framework/router)

[angular api](https://angular.io/api?type=directive)

## upgrade/static (1)



## customer directive

建立一個客制化的 directive

```shell
$ ng g directive [NEW_DIRECTIVE]
```

下列是一個監聽 input event 來改變數值寫法

```typescript
import { Directive, ElementRef, HostListener, Input } from '@angular/core';
import { NgControl } from '@angular/forms';

@Directive({ selector: '[appOnlyNumber]' })

export class OnlyNumberDirective {
    @Input() includeFloat: boolean = false;
    @Input() floatLength: number = -1;
    constructor(private el: ElementRef, private control: NgControl) {}

    private run() {
        let element = this.el.nativeElement as HTMLInputElement;
        let re = this.includeFloat ? /[^\d.]/g : /[^\d]/g;
        const overTwoDots = element.value.split('').filter((item) => item === '.').length > 1;
        if (overTwoDots) {
            const newValue = element.value.split('').slice(0, -1).join('');
            this.control.control.setValue(newValue);
            return;
        }
        const newValue = element.value.replace(re, '');
        this.control.control.setValue(newValue);
    }

    @HostListener('input', ['$event'])
    onInput() {
        this.run();
    }

    ngOnDestroy(): void {
        window.removeEventListener('input', this.onInput.bind(this));
    }
}

```



---

## Other

### how to add image in assets in angular

```html
<img [src]="imageSrc" [alt]="imageAlt" />

<img src="{{imageSrc}}" alt="{{imageAlt}}" />
```

```js
export class sample Component implements OnInit {
   imageSrc = 'assets/images/iphone.png'
   imageAlt = 'iPhone'
}
```
