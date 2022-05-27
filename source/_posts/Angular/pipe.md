---
title: "[Angular] - Pipe"
date: 2022-05-27 00:23:21
tags: angular
categories: FrontEnd
---

> angular 原生的 number 需要特別去看一下

## Common (13)

1. AsyncPipe
2. DecimalPipe
3. JsonPipe
4. PercentPipe
5. UpperCasePipe
6. CurrencyPipe
7. I18nPluraPipe
8. KeyValuePipe
9. SlicePipe
10. DatePipe
11. I18nSelectPipe
12. LowCasePipe
13. TitleCasePipe

<!--more-->

# Pipe

```tsx
{{today | date:'yyyy/MM/dd HH:mm:ss'}}
```

當然，現在有很多套件其實也都可以很輕鬆地辦到，但其實 Angular 除了 DatePipe 之外，很貼心地提供了非常多類似的 Pipe 如：

-   處理貨幣單位非常方便的  [CurrencyPipe](https://angular.io/api/common/CurrencyPipe)
-   自動 JSON 格式化的  [JsonPipe](https://angular.io/api/common/JsonPipe)
-   幫你自動訂閱的  [AsyncPipe](https://angular.io/api/common/AsyncPipe)
-   英文大小寫處理的  [UpperCasePipe](https://angular.io/api/common/UpperCasePipe)、[LowerCasePipe](https://angular.io/api/common/LowerCasePipe)  與  [TitleCasePipe](https://angular.io/api/common/TitleCasePipe)
-   專門處理小數的  [DecimalPipe](https://angular.io/api/common/DecimalPipe)
-   小數點轉百分比很方便的  [PercentPipe](https://angular.io/api/common/PercentPipe)
-   陣列跟字串都可以用的  [SlicePipe](https://angular.io/api/common/SlicePipe)
-   多國語系處理專門的  [I18nSelectPipe](https://angular.io/api/common/I18nSelectPipe)  與  [I18nPluralPipe](https://angular.io/api/common/I18nPluralPipe)
-   暫時想不到用途的  [KeyValuePipe](https://angular.io/api/common/KeyValuePipe)

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
