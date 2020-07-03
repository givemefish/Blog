---
title: Script tag中的async和defer屬性
date: 2020-07-03 13:20:01
tags: javascript
---
HTML5的script tag新增了兩個屬性async和defer

* async
  非同步地去請求外部腳本, 下載完成後會中斷HTML解析並立刻執行腳本, 執行後再恢復HTML解析
* defer
  非同步地去請求外部腳本, 但會等瀏覽器做完HTML解析完後才執行(但早於DOMContentLoaded)

![async & defer](https://html.spec.whatwg.org/images/asyncdefer.svg)
  

由於async無法確保在執行腳本時DOM已經渲染完成, 因此比較適合用在非UI的library(例如Google Analytics), 反之, 如果想要執行腳本時確保DOM已經渲染完成, 應該使用defer