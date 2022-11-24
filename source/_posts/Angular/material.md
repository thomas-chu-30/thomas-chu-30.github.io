---
tags: [angular]
title: material
date: 2022-05-27 00:23:21
categories: FrontEnd
---



## 引用 mat 樣式

```html

<mat-form-field>
  <mat-label>Input</mat-label>
  <input matInput>
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



## Datepicker

### changeEvent

```html
<input (dateChange)="change()"/>
```



```html
<mat-form-field appearance="fill">
  <mat-label>Input & change events</mat-label>
  <input matInput [matDatepicker]="picker"
         (dateInput)="addEvent('input', $event)" (dateChange)="addEvent('change', $event)">
  <mat-hint>MM/DD/YYYY</mat-hint>
  <mat-datepicker-toggle matSuffix [for]="picker"></mat-datepicker-toggle>
  <mat-datepicker #picker></mat-datepicker>
</mat-form-field>

<div class="example-events">
  <div *ngFor="let e of events">{{e}}</div>
</div>
```

```	js
import {Component} from '@angular/core';
import {MatDatepickerInputEvent} from '@angular/material/datepicker';

/** @title Datepicker input and change events */
@Component({
  selector: 'datepicker-events-example',
  templateUrl: 'datepicker-events-example.html',
  styleUrls: ['datepicker-events-example.css'],
})
export class DatepickerEventsExample {
  events: string[] = [];

  addEvent(type: string, event: MatDatepickerInputEvent<Date>) {
    this.events.push(`${type}: ${event.value}`);
  }
}
```



## customer svg icon

```javascript
import { HttpClientModule } from "@angular/common/http";
@NgModule({
  imports: [
    HttpClientModule
  ]
})
export class AppModule {}
```
```javascript
import { Component } from '@angular/core';
import { MatIconRegistry } from "@angular/material/icon";
import { DomSanitizer } from "@angular/platform-browser";
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  
  constructor(
    private matIconRegistry: MatIconRegistry,
    private domSanitizer: DomSanitizer
  ) {
    this.matIconRegistry.addSvgIcon(
      "musicon",
      this.domSanitizer.bypassSecurityTrustResourceUrl("../assets/headphone.svg")
    );
  }
}
```

```html
<mat-icon svgIcon="musicon"></mat-icon>
```

[參考文章](https://www.positronx.io/angular-material-8-icons-tutorial-with-real-world-examples/ )

