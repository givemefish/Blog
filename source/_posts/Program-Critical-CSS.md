---
title: Critical CSS
date: 2020-07-03 13:59:58
tags: css
---
習慣上我們會將外部CSS的連結放在head中，但CSS的下載需要時間，因此瀏覽器首次渲染時會看到畫面上出現空白頁面，比較好的做法是將首次渲關鍵的最小CSS集合(Critical CSS)獨立出來，以inline的方式放到head中，剩餘CSS則可用異步的方式加載。

```html
<style>
// Critical CSS
</style>
<link rel="preload" href="non-critical.css" as="style" onload="this.rel='stylesheet'"/>
```