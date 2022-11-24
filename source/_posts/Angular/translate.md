---
tags: [angular]
title: i18n tranlate
date: 2022-05-27 00:23:21
categories: FrontEnd
---

## template 引用 i18n

透過用 pipe

<!--more-->

```html
<p>{{ 'global.dialog.blacklist.title' | translate }}</p>
```

透過 js 直接翻譯

```javascript
this.translate.instant("global.dialog.blacklist.title");
```

比較不推薦的寫法

```html
<element [translate]="'id'"></element> <element translate>id</element>
```

## translate parameters

```json
{
    "demo": {
        "title": "Translation demo",
        "text": "This is a simple demonstration app for ngx-translate",
        "greeting": "Hello {{name}}!"
    }
}
```

```java
console.log(translate.instant('demo.greeting', {name: 'John'}));
```

```html
<p>{{ 'demo.greeting' | translate : {name: 'John'} }}</p>
<li [translate]="'demo.greeting'" [translateParams]="{name: 'John'}"></li>
```
