---
title: models
tags: [angular]
date: 2022-05-27 00:23:21
categories: FrontEnd
---

這個資料夾通常是放 modules 常用到的 class 用來定義 `interface` `type` `extend class` ，為了方便使用所以特別拉出來

<!--more-->

## class

1. 可以定義 fields, 也可以有建構子, 可用於檢查資料欄位

```typescript
const rawPayload = { ... }
const payload = new Class(rawPayload)
this.apiPostService.subscribe((res) => {
	console.log(res)
})
```

2. 可直接繼承 class 定義的變數和 function

```typescript
export class ProductsBasic {
	public openLoadingImg: boolean = false
	constructor(){}
	...
}
```

```typescript
import { Category, Products, ProductsBasic } from 'src/app/modules/emarket/models/products-basic';

export class ProductsPageComponent extends ProductsBasic implements OnInit {
		...
}
```

## interfece

命名的時候可在前面寫一個 prefix `I` 來定義這個是 interface

1. 可以定義 fields, 可用於檢查資料欄位

```typescript
interface ISuggestedGroup {
    path: string;
    title_en: string;
    title: string;
    count: number;
    children: ISuggestedGroup[];
}
```

2. 可以規定統一需要實作的 function

```typescript
export interface IBasicResponse<T> {
    ReturnCode: number;
    data: T;
    status: string;
}
```

```typescript
interface IMenuData {
    manufacturers: IManufacturer[];
    applications: IManufacturer[];
    functions: IManufacturer[];
    components: IManufacturer[];
}
const { data } = await useFetch<IBasicResponse<IMenu>>("/api/config/getMenu");
```

## type

1. 可以定義 fields, 可用於檢查資料欄位

```typescript
type SizeType = "sm" | "base" | "md" | "md-bold" | "lg";
```

## enum (列舉)

1. 用於定義選單資料
2. 用於定義某些欄位只能存特定 string

```typescript
export enum PaymentMethod {
    Stripe = "Stripe",
    Paypal = "Paypal",
    WireTransfer = "WireTransfer",
    CashCoupon = "Cash Coupon",
}
```

```typescript
switch (method) {
	case PaymentMethod.Stripe:
		...
		break;
	case PaymentMethod.Paypal:
		...
		break;
	default:
		...
}
```

---

## 使用情境

1. 與後端 API 溝通使用，可以是 request payload 或 response
   可用於檢查資料，當資料欄位修改時，可以依賴 IDE 做檢查，ng 編譯也會檢查

2. 可用於選單的製作

3. 可用於定義某資料欄位的限定值

https://medium.com/@notwist123/typescript-%E5%88%97%E8%88%89%E5%9E%8B%E5%88%A5-enumerate-96fc2eedd581
