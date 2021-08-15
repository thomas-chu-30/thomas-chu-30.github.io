---
title: tailwind-vs-windicss
date: 2021-08-15 17:24:44
tags:
---

> 信相前端工程師在切版下過一點功夫的人，一定都聽過 tailwind css ，但不一定有聽過 windicss ，這兩個東西都被稱作是下一個世代的 css ，今天來比較兩個的差異。
>
> 本文章不會說明太多的寫法，只會針對差別來作一個比較

<!--more-->

## tailindcss vs windicss 看看誰比較狂

|                                                                                      |                Tailwind                |             Windicss              |
| -----------------------------------------------------------------------------------: | :------------------------------------: | :-------------------------------: |
|                                                                               支援度 | Angular, Vue,React, Nuxt, Next, larval |         Vue, Nuxt, Svelte         |
| [斷點 Break point](/2021/08/15/tailwind-vs-windicss/#%E6%96%B7%E9%BB%9E-Break-point) |       只能依照 config 的法式撰寫       |  輕鬆的變換 breakpointer 的寫法   |
|                                         [CSS](/2021/08/15/tailwind-vs-windicss/#CSS) |          一般你想的到都有支援          | 比起 tailwind 有更多的 css 支援度 |
|              [討論度](/2021/08/15/tailwind-vs-windicss/#%E8%A8%8E%E8%AB%96%E5%BA%A6) |         較多人討論，進版進度快         |      討論度沒有 tailwind 高       |
|   [未來發展](/2021/08/15/tailwind-vs-windicss/#%E6%9C%AA%E4%BE%86%E7%99%BC%E5%B1%95) |           開始有 UI 系統出現           |     在寫法上有更好的歸類方式      |

## 斷點 Break point

### tailwind

預設是使用 min-width 的方式去作切版，也可以自己設定 max-width

```js
// tailwind.config.js
module.exports = {
  theme: {
    screens: {
      sm: "640px",
      // => @media (min-width: 640px) { ... }

      md: "768px",
      // => @media (min-width: 768px) { ... }

      lg: "1024px",
      // => @media (min-width: 1024px) { ... }

      xl: "1280px",
      // => @media (min-width: 1280px) { ... }

      "2xl": "1536px",
      // => @media (min-width: 1536px) { ... }
    },
  },
};
```

### windicss

預設也和 tailwind 一樣，但可用 `<` `@` ，直接變為 max-width 和 max-width & min-width，可以說是非常的方便。

```html
<div sm:bg-red-500 @sm:hover:bg-green-300 dark:bg-white></div>
```

[windicss docs](https://windicss.org/utilities/variants.html#screen-variants)

## CSS

`tailwind css` 基本上可說是該有的都有了，只是`windicss` 更狂，有更多的 effect css ，如下列：

- [Mix Blend Mode](https://windicss.org/utilities/effects.html#mix-blend-mode)

- [Caret Color](https://windicss.org/utilities/behaviors.html#caret-color)

- [Image Rendering](https://windicss.org/utilities/behaviors.html#image-rendering)

- [ List Style Type](https://windicss.org/utilities/behaviors.html#list-style-type)

## 討論度

Tailwind css 在這個上面比較熱絡，也有 youtube, Facebook 的社群可以參考，windicss 在這個上更比相較比較遜色一點，雖然在 tailwind 還沒有 jit mode 的時候，tailwind 的作者還去請教 windicss 的作者是如何作到速度不變慢，還可以持續開發。

<iframe width="560" height="315" src="https://www.youtube.com/embed/elgqxmdVms8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## 未來發展

Tailwind 在 1.9 到 2.0 可以說是有一個很大的跳躍，因為多了一個 jit mode 加速了，編譯的速度，不然過去 complier 的時候絕對讓你懷疑人生，在來也加上了 UI 系統，雖然自己切的東西最可以改，但是有時候為速度，還是要有一個寫的東西，這樣子比較可加速開發。

[Beautiful UI components](https://tailwindui.com/)

[tailwindcss mile stone](https://blog.tailwindcss.com/)

Windicss 在寫法上越來越有規劃的去撰寫你的`css`

```html
<button class="bg-blue-400 hover:bg-blue-500 text-sm text-white font-mono font-light py-2 px-4 rounded border-2 border-blue-200 dark:bg-blue-500 dark:hover:bg-blue-600">
  Button
</button>
```

在這個瞬間你可以沒有辦法看到這個 `button` 的樣式，但是如果你換成這樣子呢？

```html
<button
  bg="blue-400 hover:blue-500 dark:blue-500 dark:hover:blue-600"
  text="sm white hover:blue-500"
  font="mono light"
  p="y-2 x-4"
  border="2 rounded blue-200 hover:blue-500"
>
  Button
</button>
```

真的是很想給 windicss 一個起立掌聲 ( 拍手 )

[WindiCSS v3.0 now in Beta](https://windicss.org/posts/v30.html)

## 小結

這兩個神器只能說，各有好壞，只是 windicss 的支援度，可能在開發專案上遇到一點點界線，不然其它的地方覺得都是很優秀的，但沒辦法現行的話可能還是會以 tailwind 為首選，同時也是希望 windicss 可以把這個小缺點補上。

## 相關文章

[Windi CSS - Tailwind CSS 的上位替代](https://lucas-yang.vercel.app/post/windicss/)
