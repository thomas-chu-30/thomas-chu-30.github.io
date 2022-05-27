---
title: "[Angular] - Form"
date: 2022-05-27 00:23:21
tags: angular
categories: FrontEnd
---

## 引用 mat 樣式

<!--more-->

```html
<mat-form-field>
    <mat-label>Input</mat-label>
    <input matInput />
</mat-form-field>

<mat-form-field>
    <mat-label>Select</mat-label>
    <mat-select>
        <mat-option value="one">First option</mat-option>
        <mat-option value="two">Second option</mat-option>
    </mat-select>
</mat-form-field>

<mat-form-field>
    <mat-label>Textarea</mat-label>
    <textarea matInput></textarea>
</mat-form-field>
```

## form 表單

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

[https://www.tektutorialshub.com/angular/angular-formbuilder-in-reactive-forms/](https://www.tektutorialshub.com/angular/angular-formbuilder-in-reactive-forms/)

## FormGroup

How do I restrict an input to only accept numbers?

```jsx
<input type="number" ng-model="myText" name="inputName">
```

[How do I restrict an input to only accept numbers?](https://stackoverflow.com/questions/14615236/how-do-i-restrict-an-input-to-only-accept-numbers)

### Nested FormGroup

```jsx
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

## Validations

[Angular](https://angular.io/api/forms/Validators#compose)

```jsx
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

```javascript
this.fromName.get("formControlName").setValidators([Validators.required]);
//setting validations
this.fromName.get("formControlName").setErrors({ required: true });
//error message
this.myForm.controls["controlName"].clearValidators();
//clear valiations
this.fromName.updateValueAndValidity();
//update validation
```

[Angular reactive forms set and clear validators](https://stackoverflow.com/questions/51300628/angular-reactive-forms-set-and-clear-validators)

[https://www.tektutorialshub.com/angular/how-to-add-validators-dynamically-using-setvalidators-in-angular/](https://www.tektutorialshub.com/angular/how-to-add-validators-dynamically-using-setvalidators-in-angular/)

```jsx
private destroy$: ReplaySubject<boolean> = new ReplaySubject(1);
```

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

清楚不需要 error style 可以把此方法，我原本設用的 error 移除

```javascript
this.addProductForm.controls["part_no"].setErrors(null);
```

```javascript
note;
const pattern = /[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6}/;
// REF: https://www.w3resource.com/javascript/form/email-validation.php
const pattern = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;
```

## Reset Reactive Form

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

## ValueChange

[value change](https://www.tektutorialshub.com/angular/valuechanges-in-angular-forms/)

## Custom Async Validators

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
