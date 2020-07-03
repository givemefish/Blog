---
title: 最佳化JavasScript載入速度
date: 2020-07-03 11:15:39
tags: javascript
---
# 載入JavaScript時常碰到的問題

1. 如果頁面上有API request, 要等到JavaScript bundle被下載到瀏覽器後才會執行
2. 如果頁面上有API request, 要等到request回傳完成後才會開始渲染頁面內容
3. 混用輔助的第三方套件(如Google分析等)的API request而影響主要頁面的載入和渲染

以下探討一些簡單的處理方式

## 預先載入API資料
1. 最佳的做法是將API資料先在server端產生, 然後直接含在HTML頁面中, 這得後端配合
2. 另一個做法是直接寫inline script在HTML頁面中來提前取得資料
    ```html
    <div id="app"></div>
    <script>
      fetchData();
      function fetchData() {
        window._data = fetch('/api/data')
          .then((response) => response.json());
      }  
    </script>
    <script src="/vender.xxx.js"></script>
    <script src="/app.xxx.js"></script>
    ```


## 延遟第三方套件的API request時機
一個簡單的方法是用timeout來延遲第三方套件的API request
```JavaScript
// Before
async function installThirdParties() {
  ga('create', 'UA-XXXXX-Y', 'auto');
}

// After
async function installThirdParties() {
  setTimeout(() => {
    ga('create', 'UA-XXXXX-Y', 'auto');
  }, 15 * 1000);
}
```
```setTimeout```並不是最佳的方法, 但對一般頁面也足夠使用了, 更好的方法是自行定義一個「頁面完全載入」的事件, 在該事件被觸發時才載入第三方套件.
