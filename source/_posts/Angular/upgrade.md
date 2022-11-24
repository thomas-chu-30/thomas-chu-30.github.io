---
title: upgrade 所遇到的問題
tags: [angular]
date: 2022-05-27 00:23:21
categories: FrontEnd
---



## 11 升 12 所遇到的坑

cpu 附載過高問題

```javascript
// service/index.ts
server.engine(
	'html',
	ngExpressEngine({
		inlineCriticalCss:false,
		bootstrap: AppServerModule,
		providers: [
				{
					provide: APP_CONFIG,
					useValue: appConfig(),
				},
		],
	})
);
```



```json
"optimization": {
	"scripts": true,
	"styles": {
		"minify": true,
		"inlineCritical": false
	},
	"fonts": true
},
```



https://0xdbe.github.io/AngularSecurity-DisableInlineCriticalCSS/

https://github.com/angular/angular-cli/issues/20864