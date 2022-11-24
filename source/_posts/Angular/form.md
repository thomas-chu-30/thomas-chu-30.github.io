---
title: Form
date: 2022-05-27 00:23:21
tags: [angular]
categories: FrontEnd
---

> *響應式表單*提供了一種模型驅動的方式來處理表單輸入，其中的值會隨時間而變化。本文會向你展示如何建立和更新基本的表單控制元件，接下來還會在一個表單組中使用多個控制元件，驗證表單的值，以及建立動態表單，也就是在執行期新增或移除控制元件。

<!--more-->

## form 表單

這裡的 require 建儀是寫在 formGroup 裡面去作理管，才可方便的在 js 中看到何為必填值。

```jsx
<form [formGroup]="subscribeForm" (ngSubmit)="submit()">
   <mat-form-field class="w-full">
       <input
           matInput
           required
           type="email"
           formControlName="email"
        />
        <mat-error> Please enter a valid email address </mat-error>
    </mat-form-field>
    <button type="submit">submit</button>
</form>
```

## invalid function

透過下列這段 checked form 是否有尚未寫好的值，或是沒有通過的 validations。

```javascript
this.formName.invalid;
```

### disable enable

可把欄位 disable 和 enable，但是特別注意 `disable()` 的值，如果直接用 `this.form.value` 會拿不到值

```javascript
this.formName.controls["control"].disable();
this.formName.controls["control"].enable();
```

如果想要拿到 `disable()` 的值，需要用 `getRawValue()` 來取得到已被 `disable()` 的值

```javascript
this.formName.getRawValue();
```

## FormGroup

How do I restrict an input to only accept numbers?

```jsx
<input type="number" ng-model="myText" name="inputName">
```

[How do I restrict an input to only accept numbers?](https://stackoverflow.com/questions/14615236/how-do-i-restrict-an-input-to-only-accept-numbers)

### Nested FormGroup

form 的表單很大的情況，希望可以有結構化的去管理資料，可以 `nest formGroup` 的方式，方便一目了然的去抓到資料

```javascript
this.contactForm = this.formBuilder.group({
    firstname: ["", [Validators.required, Validators.minLength(10)]],
    lastname: ["", [Validators.required, Validators.maxLength(15), Validators.pattern("^[a-zA-Z]+$")]],
    email: ["", [Validators.required, Validators.email]],
    gender: ["", [Validators.required]],
    isMarried: ["", [Validators.required]],
    country: ["", [Validators.required]],
    address: this.formBuilder.group({
        city: ["", [Validators.required]],
        street: ["", [Validators.required]],
        pincode: ["", [Validators.required]],
    }),
});
```

[https://www.tektutorialshub.com/angular/angular-formbuilder-in-reactive-forms/](https://www.tektutorialshub.com/angular/angular-formbuilder-in-reactive-forms/)

## Validations

下列是 angular 在 formGroup 中提供的 validations 的方式，當然也可以自己去寫 customer 的 validation function

[Angular](https://angular.io/api/forms/Validators#compose)

```javascript
class Validators {
  static min(min: number): ValidatorFn
  static max(max: number): ValidatorFn
  static required(control: AbstractControl): ValidationErrors | null
  static requiredTrue(control: AbstractControl): ValidationErrors | null
  static email(control: AbstractControl): ValidationErrors | null
  static minLength(minLength: number): ValidatorFn
  static maxLength(maxLength: number): ValidatorFn
  static pattern(pattern: string | RegExp): ValidatorFn
  static nullValidator(control: AbstractControl): ValidationErrors | null
  static compose(validators: ValidatorFn[]): ValidatorFn | null
  static composeAsync(validators: AsyncValidatorFn[]): AsyncValidatorFn | null
}
```

### updateValidations

setErrors 如果是 null 的情況下，會把原本的 required 的設定也都拿掉，所以要特別小心

```javascript
this.formName.get("formControlName").setValidators([Validators.required]);
//setting validations
this.formName.get("formControlName").setErrors({ required: true });
this.formName.get("formControlName").setErrors({ required: false }); // 會有 error 的style 不會有 msg
this.formName.get("formControlName").setErrors(null); // 清除 errors 的方法
//error message
this.myForm.controls["controlName"].clearValidators();
//clear valiations
this.formName.updateValueAndValidity();
//update validation
this.formName.controls.reset();
// 把 form 表中的資料回復到最一開始的樣子
```

**NOTE** 如果是在另一個 component 中要去 control 另一個 form 給它 setErrors 的話可以加上面這一段，這樣子才可以正常的設定 error

```javascript
this.formName.markAsTouched({ onlySelf: true });
```

[Angular reactive forms set and clear validators](https://stackoverflow.com/questions/51300628/angular-reactive-forms-set-and-clear-validators)

[https://www.tektutorialshub.com/angular/how-to-add-validators-dynamically-using-setvalidators-in-angular/](https://www.tektutorialshub.com/angular/how-to-add-validators-dynamically-using-setvalidators-in-angular/)

### hasError

在操作 js 的時候，需要有一個特定的 error style 可以用 `setErrors` 來設定 `boolean` 讓 `template` 來使用

```javascript
this.productsForm[index].controls["unit_price"].setErrors({ bottomPrice: true });
```

```html
<mat-error *ngIf="productsForm[index].get('unit_price').hasError('bottomPrice')">
    <span>Please enter bottomPrice.</span>
</mat-error>
```

清除不需要 error style 可以把此方法，我原本設用的 error 移除

```javascript
this.addProductForm.controls["part_no"].setErrors(null);
```

```javascript
note;
const pattern = /[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6}/;
// REF: https://www.w3resource.com/javascript/form/email-validation.php
const pattern = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;
```

### Custom & Async Validators

#### Custom Validators

#### Custom Async Validators

```javascript
import { Injectable } from '@angular/core';
import {AbstractControl, FormControl, FormGroup, ValidationErrors} from '@angular/forms';
import {Observable, of} from 'rxjs';
import {delay, map} from 'rxjs/operators';

@Injectable({
  providedIn: 'root'
})
export class ZipcodeService {
  private validZipcodes = ['00001', '00002', '00003', '00004'];

  fakeHttp(value: string) {
    return of(this.validZipcodes.includes(value)).pipe(delay(5000));
  }
}
```

```javascript
import { ZipcodeService } from "./zipcode.service";
import { AbstractControl, AsyncValidatorFn, ValidationErrors } from "@angular/forms";
import { Observable } from "rxjs";
import { map } from "rxjs/operators";

export class ZipcodeValidator {
    static createValidator(zipcodeService: ZipcodeService): AsyncValidatorFn {
        return (control: AbstractControl): Observable<ValidationErrors> => {
            return zipcodeService.fakeHttp(control.value).pipe(map((result: boolean) => (result ? null : { invalidAsync: true })));
        };
    }
}
```

```javascript
import {Component, OnInit} from '@angular/core';
import { FormControl, FormGroup, Validators} from '@angular/forms';
import {ZipcodeService} from './zipcode.service';
import {ZipcodeValidator} from './zipcode-validator';

@Component({
  selector: 'app-async-validator-demo',
  templateUrl: './async-validator-demo.component.html',
  styleUrls: ['./async-validator-demo.component.scss']
})
export class AsyncValidatorDemoComponent implements OnInit {
  address: FormGroup;
  zipcodeSyncValidators = [
    Validators.required,
    Validators.pattern('\\d{5}')
  ];

  constructor(private zipcodeService: ZipcodeService) {}

  ngOnInit(): void {
    this.address = new FormGroup({
      zipcode: new FormControl('',
       this.zipcodeSyncValidators,
       ZipcodeValidator.createValidator(this.zipcodeService))
    });
  }
}
```

[Angular: Custom Async Validators](https://medium.com/@rinciarijoc/angular-custom-async-validators-13a648d688d8)

### cross reative form

https://offering.solutions/blog/articles/2020/05/03/cross-field-validation-using-angular-reactive-forms/#adding-custom-validators-to-a-single-form-control

## Reset Reactive Form

有些情況下，submit form 之後，要在清除 form 的資料，可用下列的方式去作 clear 的動作。

```html
<form [formGroup]="addProductForm" (ngSubmit)="addProduct()" #formDirective="ngForm">...</form>
```

```javascript
export class CorporateQuotationPageComponent implements OnInit {
   @ViewChild('formDirective') formDirective;
	 ...
   resetForm() {
  		this.formDirective.resetForm(); //重新的把值清空
   }
}
```

**reset() vsj resetForm() ？？**

## ValueChange

```javascript
this.formName.controls["control"].setValue(data);
```

### EmitEvent & ValueChanges

coming soon ...

### OnlySelf & ValueChanges

coming soon ...

[value change 參考文章](https://www.tektutorialshub.com/angular/valuechanges-in-angular-forms/)
