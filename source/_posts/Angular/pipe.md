---
title: Pipe
date: 2022-05-27 00:23:21
tags: [angular]
categories: FrontEnd
---

> angular 原生的 number 需要特別去看一下 decimaPipe

<!--more-->

## Common Pipe

`pipe` 的使用如下，也可以加上 params 的透過`:` 來傳入

```tsx
{{today | date:'yyyy/MM/dd HH:mm:ss'}}
```

下列是 `angular` 所提供的 `pipe` ，如下列：

-   處理日期 format 的 [DatePipe](https://angular.io/api/common/DatePipe)
-   處理貨幣單位非常方便的  [CurrencyPipe](https://angular.io/api/common/CurrencyPipe)
-   自動 JSON 格式化的  [JsonPipe](https://angular.io/api/common/JsonPipe)
-   幫你自動訂閱的  [AsyncPipe](https://angular.io/api/common/AsyncPipe)
-   英文大小寫處理的  [UpperCasePipe](https://angular.io/api/common/UpperCasePipe)、[LowerCasePipe](https://angular.io/api/common/LowerCasePipe)  與  [TitleCasePipe](https://angular.io/api/common/TitleCasePipe)
-   專門處理小數的  [DecimalPipe](https://angular.io/api/common/DecimalPipe)
-   小數點轉百分比很方便的  [PercentPipe](https://angular.io/api/common/PercentPipe)
-   陣列跟字串都可以用的  [SlicePipe](https://angular.io/api/common/SlicePipe)
-   多國語系處理專門的  [I18nSelectPipe](https://angular.io/api/common/I18nSelectPipe)  與  [I18nPluralPipe](https://angular.io/api/common/I18nPluralPipe)
-   暫時想不到用途的  [KeyValuePipe](https://angular.io/api/common/KeyValuePipe)

### DecimalPipe [ | number ]

使用方式如：

```javascript
{{ value_expression | number [ : digitsInfo [ : locale ] ] }}
```

-   value 是輸入值
-   number 是這個 Pipes 元件的名稱
-   digitsInfo 為字串型態的參數，非必填項目
    -   格式如 `{minIntegerDigits}.{minFractionDigits}-{maxFractionDigits}`
    -   minIntegerDigits：在小数点前的最小位数。默认为 1。
    -   minFractionDigits：小数点后的最小位数。默认为 0。
    -   maxFractionDigits：小数点后的最大为数，默认为 3。
-   locale 為字串型態的參數，非必填項目
    -   用來設定這一串數字要用哪一個地區的數值格式呈現

因此可以按照官方提供的範例，複製一份並且在 Template 內隨意找個地方貼上玩看看：

**Template**

```html
<div>
    <!--output '2.718'-->
    <p>e (no formatting): {{e | number}}</p>

    <!--output '002.71828'-->
    <p>e (3.1-5): {{e | number:'3.1-5'}}</p>

    <!--output '0,002.71828'-->
    <p>e (4.5-5): {{e | number:'4.5-5'}}</p>

    <!--output '0 002,71828'-->
    <p>e (french): {{e | number:'4.5-5':'fr'}}</p>

    <!--output '3.14'-->
    <p>pi (no formatting): {{pi | number}}</p>

    <!--output '003.14'-->
    <p>pi (3.1-5): {{pi | number:'3.1-5'}}</p>

    <!--output '003.14000'-->
    <p>pi (3.5-5): {{pi | number:'3.5-5'}}</p>

    <!--output '-3' / unlike '-2' by Math.round()-->
    <p>-2.5 (1.0-0): {{-2.5 | number:'1.0-0'}}</p>
</div>
```

Template 有用到 `e` 以及 `pi` 這兩個內嵌繫結，因此必須在 class 內補上這兩個屬性。

```javascript
export class AppComponent {
    inputValue = "";
    pi: number = 3.14;
    e: number = 2.718281828459045;
}
```

> 運行開發伺服器，看看效果如何～

[![img](https://i.imgur.com/zqZBBLG.png)](https://i.imgur.com/zqZBBLG.png)

-   第一個結果 e 輸出是 2.718 ，對照後也就是說預設的情況下 DecimalPipe 會輸出小數點後三位的數字，其餘全部捨去。
    -   而這個結果是因為沒有填寫任何參數，是參數的默認值導致
-   第二個結果傳入一個參數 `3.1-5` ，對照上面的格式與參數解釋後，得到結果 e 為 002.71828

> 可透過修改第一個參數達成想要的數字格式。

-   第四個結果，傳入的第二個參數為 fr ，代表採用法國的數值格式
    -   在法國，小數點是當作千分號使用，而千分號則是使用空白替代
    -   透過不同的國家的 locale id 就可以轉換成對應的地區數值格式
        -   台灣為 zh-TW
        -   日本為 jp

**不僅僅第一個參數可以利用，配合第二個參數一起使用才是王道。**

> 而這個 Pipes 元件好玩的地方是，它的名稱叫做 DecimalPipe ，但實際使用卻是輸入 number ，這是容易搞混的地方要特別注意。

## Customer pipe

下列是客製化 pipe 的用法

```tsx
import { Pipe, PipeTransform } from "@angular/core";

/*
 * Raise the value exponentially
 * Takes an exponent argument that defaults to 1.
 * Usage:
 *   value | exponentialStrength:exponent
 * Example:
 *   {{ 2 | exponentialStrength:10 }}
 *   formats to: 1024
 */
@Pipe({ name: "exponentialStrength" })
export class ExponentialStrengthPipe implements PipeTransform {
    transform(value: number, exponent: string): number {
        let exp = parseFloat(exponent);
        return Math.pow(value, isNaN(exp) ? 1 : exp);
    }
}
```

[custom-pipe-demo - StackBlitz](https://stackblitz.com/edit/custom-pipe-demo?file=app%2Fpipes%2Ftruncate.pipe.ts)

[[從 0 開始的 Angular 生活]No.22 使用 Pipes 管線元件](https://pvt5r486.github.io/f2e/20190529/2426750085/)

## 在 JS 中 call pip function

```jsx
import { FirstUpperCasePipe } from "src/app/pipes/first-upper-case.pipe";
// new 一個新的 class
const slugUpperCase = new FirstUpperCasePipe().transform(this.slug);
```
