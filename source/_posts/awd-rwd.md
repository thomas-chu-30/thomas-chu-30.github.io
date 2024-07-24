---
tags: [rwd, awd]
categories: 生活長知識
title: 什麼是 RWD？ RWD 跟 AWD 有什麼不同？
---

![RWD or AWD](https://www.da-vinci.com.tw/uploads/images/cache/a8c2eb45f4d5776ca28ca0f831041c29-1000x500c00-1-1.png)

## 網站不能沒有 RWD、AWD

沒有 RWD、AWD 的網站到底會怎樣？先講結論，網站流量慢慢會掉下來，因為 Google 說「演算法以行動網站為主」，網站沒有行動網站流量就會慢慢消失，RWD 跟 AWD 都是行動網站，所以網站一定要有 RWD 或 AWD，現在用行動裝置上網的比例超過 80%，簡單來說沒有手機版的網站等於宣告死刑，沒有手機版的網站請趕快改版，即使是 B2B 網站，RWD、AWD 都不是新技術，已經是成熟的網頁設計方式，而且套版網站設計費沒有很高，趕快改版才是當務之急。
〈**延伸閱讀：**[網頁設計公司不會告訴你的 5 個真相](https://www.da-vinci.com.tw/tw/blog/webdesign-5fact)〉

<!--more-->
<!--truncate-->

### 2020 年台灣行動上網人口

![沒有RWD網站無法生存](https://www.da-vinci.com.tw/uploads/editor/files/mobile-network-use.png)
_來源：TWNIC_

## RWD 是甚麼?

RWD 的英文全名是 Responsive Web Design，中文翻譯是「響應式網頁設計」，簡單來說 RWD 就是「同一個網址可同時出現手機、平板、桌機的網站的設計方法」，隨著各種裝置銀幕的大小，自動會顯示不同的網站尺寸，用手機就跑手機版網站，用桌機就跑桌機版網站，用平板就跑平板網站，RWD 就是把三個版本網站合而為一。怎麼知道網站是不是 RWD? 你可以實驗一下，把瀏覽器的視窗拉一拉就知道了，RWD 會讀取「同一個 CSS」，會自動排列網站，請點擊看下方影片就知道可以 RWD 怎麼變化，網站如果是 AWD 或是傳統的手機版網站，是不會這樣變化版面的。

### RWD 自動放大縮小網站尺寸

```html
<video controls="" height="240" width="320" style="box-sizing: inherit; display: inline-block; position: absolute; width: 810px; height: 506.25px; left: 0px; top: 0px;"></video>
```

## AWD 是甚麼?

AWD 的英文全名是 Adaptive Web Design，中文翻譯是「自適應網頁設計」，AWD 跟 RWD 外觀、使用起來都沒有太大差別，因為 AWD 跟 RWD 一樣都是「以同一個網址同時出現手機、平板、桌機的網站設計方法」，如果你有看上面的小短片就知道，視窗拉動的時候以 RWD 設計的網站是會放大縮小的，但是 AWD 不會放大縮小，因為 AWD 是會讀取「多個不同的 CSS」，所以只會在真正的裝置上顯示自適應的頁面。
**〈延伸閱讀：**[網頁設計與 SEO 的完美整合](https://www.da-vinci.com.tw/tw/blog/seo-webdesign)〉

**CSS 是甚麼?**
CSS，英文是 Cascading Style Sheets，中文稱做：樣式表、級聯樣式表、串接樣式表、階層式樣式表，CSS 不能單獨使用，必須與 HTML 或 XML 一起協同工作，CSS 樣式表是在定義網站的外觀、樣式、字體大小、字體粗細、字體顏色、元素對齊、定位...這些元素，CSS 主要目的就是設定網頁的布局、設定網頁的樣式，CSS 樣式定義完成之後，就可以用在全部的網站，讓網站不用一頁一頁設定字體、顏色、位置、樣式....，可以加速網站設計，RWD 是共用 CSS，AWD 則是分開 CSS，CSS 樣式工作都是由前端工程師負責製作。

**〈延伸閱讀：**[網頁設計為什麼需要前端工程師？](https://www.da-vinci.com.tw/tw/blog/front-end-webdesign)〉

## RWD、AWD 有什麼不同？

不刻意去辨識之下，RWD、AWD 從外觀是看不出來差異的，雖然都是同一個網址跑多個版本網站，但兩者在技術上是有差異的，像是 RWD 是讀同一個 CSS，AWD 則讀取不同 CSS，AWD 可以輕易讓不同的內容在手機版上，AWD 效能略優於 RWD，AWD 可以針對行動版做 UX 優化，RWD 製作費較便宜，且容易維護，RWD 開發時間短，比較不會出現重複內容，RWD 有較多的框架開發工具，使用率較高...，以上都是他們之間的差異，下面比較表就可以清楚知道他們的差異。

〈**延伸閱讀：**[網頁設計的使用者體驗(UX)如何執行？](https://www.da-vinci.com.tw/tw/blog/ux-webdesign) 〉

|       項目       | RWD 響應式設計 | AWD 自適應設計 |
| :--------------: | :------------: | :------------: |
|   不同版本網站   |   同一個網址   |   同一個網址   |
|    CSS 樣式表    |   同一個 CSS   |   不同的 CSS   |
|   網站內容一致   |    內容一樣    |     不一定     |
| 自動判斷各種裝置 |    自動判斷    |    自動判斷    |
|   行動裝置速度   |    速度中等    |    速度較快    |
| 行動裝置體驗優化 |    固定內容    |     可優化     |
| 網站製作費(客製) |      中等      |      較高      |
|   網站資料維護   |    維護容易    | 部分維護多版本 |
|     開發時間     |      快速      |    時間較長    |
|   結構重複內容   |    不會發生    |    偶爾發生    |
|   網址重新導向   |   不會重導向   |   不會重導向   |
| Google 檢索速度  |       快       |       快       |
|   適合執行 SEO   |      適合      |      適合      |
|   框架開發工具   |       多       |       少       |
|  設計公司使用率  |       高       |       低       |
|   手工網站切版   |      可以      |      可以      |

(製表: 達文西數位科技)

## RWD、AWD 應該怎麼選呢？

先講結論，如果沒有特殊的需求，用 RWD 進行網站設計就可以了。大部分的網站都不需要 AWD 這樣的模式，因為 AWD 製作費比較高，會做的人少，成本比較高，開發時間比較久，以成本效益來說，除非有需要，不然就是用 RWD 就可以了。

### 內容很多才需要用 AWD

內容很多才需要用 AWD，因為 RWD 內容只能在桌機、平板、手機之間做重新排列，內容是不能少的，所以像是像 MOMO、PCHOME...這類內容超多的網站，就必須要手機版減少內容，不然畫面會很長，所以這類大型購物網站都是用 AWD，或是用兩個不同網址的網站，企業網站、小型購物網站就比較適合 RWD，像是 Shopline、Cyberbiz 都是 RWD 製作的，內容非常多的網站才建議使用 AWD。
〈**延伸閱讀**：[套版網站看起來都很像，到底差在哪?](https://www.da-vinci.com.tw/tw/blog/detail/57)〉

### AWD 製作、維護成本高

響應式網頁設計(RWD)上線後的維護是比較容易的，AWD 維護上較繁瑣，AWD 必須在後台維護各版本的網站，製作成本 AWD 也比 RWD 貴，因為做的人比較少，開發時間也比較長，性價比來看還是 RWD 比較划算，AWD 在設計與維護上成本都比較高，也是大部分的網頁設計公司都採用 RWD 的最大原因。
**〈延伸閱讀：**[網站建置費用? 網頁設計報價為何這麼亂?](https://www.da-vinci.com.tw/tw/blog/webdesign-price)〉

### 需要更深入使用者體驗(UX)

AWD 可以對手機版做更深入的使用者體驗(UX)，針對手機使用者做內容調整與優化，讓使用流程更友善，但近年來的 RWD 設計已經趨向簡單乾淨，並以手機流程為主要設計，而且大部分的網站都不會像 momo、pchome 那樣複雜，所以 AWD 使用機會並不是很高，就算是大型購物平台也慢慢把手機版網站轉向到 APP，使用者體驗也以 APP 為主，AWD 對手機版進行優化的這個優勢已經沒有這麼明顯。
〈**延伸閱讀:** [UX/UI 不一樣，UI/UX 設計是什麼？](https://www.da-vinci.com.tw/tw/blog/ui-ux-comparison)〉

## RWD、AWD 哪一種對 SEO 比較好？

哪一種對 SEO 比較好？答案是：「兩者差距不大」，SEO 的排名規則有「SEO 以行動版網站內容為主」、「網站行動效能影響 SEO」、「網站版本之間的內容一致性會影響 SEO」，手機網站部分：AWD、RWD 兩個都有手機版，所以都符合條件。網站效能部分：AWD 手機效能略優於 RWD，這裡是 AWD 稍微優勢一些。內容一致性部分：AWD 的網站版本之間的確會因為優化，產生內容不同步，RWD 版本則是內容一致，所以在內容一致性上面，RWD 勝 AWD，在各有優缺點之下，兩者其實差異不大，主要還是要看網站的 SEO 優化程度，而不是網頁設計用了 RWD 或 AWD。
〈**延伸閱讀:** [SEO 是什麼? 簡單說讓你聽得懂](https://www.da-vinci.com.tw/tw/blog/seo-what)〉
〈**延伸閱讀:** [關鍵字排名優化最重要的 3 件事](https://www.da-vinci.com.tw/tw/blog/keyword-ranking-optimization)〉

**什麼是 PSI ？**
PSI 的英文是 PageSpeed Insights，簡稱 PSI。PSI 是 Google 提供的「檢測網站性能與速度的線上工具」，除了檢測結果以外並提供各種修改建議，分數是透過運行 Google Lighthouse 資料庫來分析網站，90 分或以上是非常好，50 到 90 中等架構，低於 50 是很差的架構，通常要執行 SEO，最少都要有 80 分以上。
【**網站 PSI 是幾分？馬上來測試** [PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/?hl=zh-TW)】

## RWD 有兩種設計方式

RWD(響應式網站設計) 分成兩種製作方式：「框架工具」跟「手工切版」，如果不考慮 SEO 跟網站效能的話，其實這兩種方式製作的網站，幾乎沒有什麼明顯差異，都可以達到 RWD 的設計呈現，但如果要針對網站效能與修改彈性，「手工切版」是遠勝於「框架工具」製作的 RWD 網站，這個可以從 Google 的 PSI 測試工具得到測試結果。
〈**延伸閱讀:** [什麼是 RWD 切版？](https://www.da-vinci.com.tw/tw/blog/front-end-webdesign)〉

### 以框架工具製作 RWD

就是選擇現成的 RWD 框架開發工具，依照既有的 RWD 模版去套用網站素材，然後將網站素材組裝網站交給客戶，後續根據客戶修改需求進行修改，好處是可以減少製作時間，因為有很多現成的模組跟效果可以用，但因為模組因素所以程式無法精簡，網站效能會比較差，還有網站修改幅度不能過大會有技術難度，常見的 RWD 框架工具有：Bootstrap、Semantic UI、Foundation、UiKit...，最多人使用的就是 Bootstrap，Bootstrap 有很多現成的版型，也使用在知名的套版與軟體，例如：Wordpress、Adobe Dreamweaver，缺點就是有「很多的累贅程式碼」，不會改的話效能會很差，AWD 就不像 RWD 有這麼多的框架工具。
〈**延伸閱讀：**[RWD 網頁設計好壞差很多](https://www.da-vinci.com.tw/tw/blog/rwd-different) 〉

### 以手工切版製作 RWD

手工切版，顧名思義就是「手工」，就是不使用 RWD 框架工具進行的切版工作，而是從無到有的產出網站的 html，既然有方便的 RWD 框架工具，為什麼要用「手工」找麻煩？主要原因就是為了有「更有效率的網站」、「網站可以方便修改」這兩件事，手工切版可以精簡程式，不會有像框架工具的「累贅程式碼」，手工切版可以有程式自主權，容易修改程式，也可以達到 HTML 最佳化，但缺點是需要更多的製作時間，從拿到網站設計圖稿，慢慢把圖片切成 HTML，整個製作時間是框架工具製作 RWD 網站的兩倍時間以上，八成以上的網頁設計公司都不會採用，但如果要執行 SEO，需要高效能 PSI 的網站，就需要手切網站。
**〈延伸閱讀：**[網站速度- SEO 優化的重要項目](https://www.da-vinci.com.tw/tw/seo-speed)〉

|      項目      | RWD 框架工具 | RWD 手工切版 |
| :------------: | :----------: | :----------: |
|  RWD 網站呈現  |     完整     |     完整     |
|   代表性工具   |   Boostrap   |     ---      |
|  程式修改彈性  |      低      |      高      |
|  設計修改彈性  |      低      |      高      |
|  PSI 效能分數  |      低      |      高      |
|    累贅程式    |      多      |      少      |
|    製作時間    |      短      |      長      |
|   現成的效果   |      多      |   需另外裝   |
|    SEO 效能    |      低      |      高      |
|  網站客製程度  |   設計客製   |   全程客製   |
| 設計公司使用率 |      高      |      低      |
|    開發成本    |      低      |      高      |

(製表: 達文西數位科技)

## 如何檢查行動版網站的狀況？

要怎麼檢視行動版網站狀況呢？可以用 Google Search Console(GSC)審查網址，Google 於 2020 年正式以行動版作為搜尋收錄與排名的基準，所以網站必須符合各種行動裝置的規則，所以可以透過 GSC 去查看網站的「行動裝置可用性」、「網站內容」、「中繼資料(Meta Data)」、「結構化資料(Structured Data)」，可以從中找出網站是不是有符合規則，如果有檢測到行動網站的錯誤，就可以根據錯誤進行修正，RWD、AWD 都可以從 Google Search Console 檢測，是 SEO 很重要的工作之一。
**〈延伸閱讀：**[SEO 排名因素有哪些？ 45 個要點一次看完](https://www.da-vinci.com.tw/tw/blog/SEO-ranking_key_points)〉

### Google 以行動網站作為索引，響應式網站變得重要

![Google以行動裝置作為索引](https://www.da-vinci.com.tw/uploads/editor/files/%E7%B6%B2%E7%AB%99%E4%BB%A5%E8%A1%8C%E5%8B%95%E7%B4%A2%E5%BC%95%E7%82%BA%E4%B8%BB.jpg)

### Google Search Console 檢查行動網站(響應式網站)

![Google Search Console檢查行動網站](https://www.da-vinci.com.tw/uploads/editor/files/gsc%E6%AA%A2%E6%9F%A5%E8%A1%8C%E5%8B%95%E8%A3%9D%E7%BD%AE%E5%8F%AF%E7%94%A8%E6%80%A7.jpg)

### 結論

RWD 網頁設計已經是最主流的網站設計方式，如果網站內容簡單可以選 RWD(響應式網頁設計)，例如: 企業網站、小型購物網站，如果是大型網站希望手機版可以單獨優化，例如: PCHOME 購物，那麼可以用 AWD 製作，一般購物網站使用 RWD 就很夠了，AWD 製作與維護成本較高，也會有資料不同步的可能，如果沒有特別的網站需求，用 RWD(響應式網站設計)是比較好的選擇，還有就是 RWD 並沒有都一樣，選擇專業的網頁設計才能達到高分數 PSI 網站，對 SEO 來說才是最佳方案。

## 參考文章

https://www.da-vinci.com.tw/tw/blog/rwd
