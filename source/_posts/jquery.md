---
title: jquery 時代的眼淚
categories: frontend
tags: jquery
---

專案遇到只要來紀念一下時代的眼淚，筆記一下，之後比較好 coding

<!--more-->
<!--truncate-->

````html
```jsx // element [ 'class' | '#class' | p | h1 ] $(element).addClass("active"); $(element).removeClass("active"); $(element).text("hello world"); $(element).html("
<p>hello world</p>
"); $(element).val(""); // clear
````

ajax

```jsx
$.ajax({
      url: "/api",
      type: "POST",
      dataType: "json",
      contentType: "application/json",
      data: JSON.stringify(data),
    })
      .done(function (res) {
				...
      })
      .fail(function (error) {
        console.error(error.responseJSON);
      })
      .always(function () {
				...
      });
```
